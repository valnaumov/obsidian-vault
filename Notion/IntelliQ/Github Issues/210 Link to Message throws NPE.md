---
Created: 2023-11-23T21:10
Updated: 2023-11-23T22:19
---
Linking to an Inbound message (ValidateMessageScenarioStep) caused a NPE.
The original problem was due to the missing actual message in `LinkToValidateMessageStepPresenter`. Inbound message was not yet received. Used a MissingNode instead. We showed the expected message in LinkToValidateMessageStepView for the reference. Actual linking should happen to the actual received message, of course.
Another problem was revealed.
When linking `NewOrderSingle`'s OrderType to an `ExecutionReport`, we get a `quickfix.FieldException`
- Exception
    
    ```JavaScript
    quickfix.FieldException: invalid character value: ${MESSAGE_FIELD:66fd01bb-aff8-4896-8581-4260efc359c6.$['OrdType']}
    	at quickfix.FieldMap.newIncorrectDataException(FieldMap.java:390)
    	at quickfix.FieldMap.getChar(FieldMap.java:237)
    	at se.suncom.multiq.plugin.fix.FixSession.getSecondLine(FixSession.java:509)
    	at se.suncom.multiq.plugin.fix.FixSession.createOutboundMessage(FixSession.java:950)
    	at se.suncom.multiq.interfaces.impl.SendMessageScenarioStep.createMessage(SendMessageScenarioStep.java:83)
    	at se.suncom.multiq.interfaces.impl.MessageScenarioStep.updateMessage(MessageScenarioStep.java:83)
    	at se.suncom.multiq.interfaces.impl.MessageScenarioStep.lambda$createForm$0(MessageScenarioStep.java:75)
    	at org.reactfx.util.NonAccumulativeStreamNotifications.lambda$head$0(NotificationAccumulator.java:134)
    	at org.reactfx.ObservableBase.notifyObservers(ObservableBase.java:68)
    	at org.reactfx.ObservableBase.notifyObservers(ObservableBase.java:57)
    	at org.reactfx.ProperEventStream.emit(ProperEventStream.java:18)
    	at org.reactfx.EventStreams$5.lambda$observeInputs$0(EventStreams.java:144)
    	at org.reactfx.value.ChangeListenerWrapper.accept(Val.java:786)
    	at org.reactfx.util.AbstractReducingStreamNotifications.lambda$head$0(NotificationAccumulator.java:248)
    	at org.reactfx.ObservableBase.notifyObservers(ObservableBase.java:68)
    	at org.reactfx.ObservableBase.notifyObservers(ObservableBase.java:57)
    	at org.reactfx.value.ValBase.invalidate(ValBase.java:32)
    	at org.reactfx.value.SimpleVar.setValue(SimpleVar.java:59)
    	at se.suncom.multiq.model.form.schema.SchemaForm.setModel(SchemaForm.java:111)
    	at se.suncom.multiq.model.form.schema.SchemaForm.lambda$null$3(SchemaForm.java:188)
    	at org.reactfx.Suspendable.suspendWhile(Suspendable.java:49)
    	at se.suncom.multiq.model.form.schema.SchemaForm.lambda$setModelFromWebView$4(SchemaForm.java:187)
    	at com.sun.javafx.application.PlatformImpl.lambda$null$177(PlatformImpl.java:295)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at com.sun.javafx.application.PlatformImpl.lambda$runLater$178(PlatformImpl.java:294)
    	at com.sun.glass.ui.InvokeLaterDispatcher$Future.run(InvokeLaterDispatcher.java:95)
    	at com.sun.glass.ui.win.WinApplication._runLoop(Native Method)
    	at com.sun.glass.ui.win.WinApplication.lambda$null$152(WinApplication.java:177)
    	at java.lang.Thread.run(Thread.java:748)
    ```
    
      
    
It complains about improper format of OrderType: `${MESSAGE_FIELD:66fd01bb-aff8-4896-8581-4260efc359c6.$['OrdType']}`. It is a link. But the message passed to getSecondLine should be already “actualized”, i.e. replaced with actual values from the linked message.
Elias’ commit should handle the `quickfix.FieldException` though.
In order to actualize a message that we’re creating in ScenarioStep, we need an instance of IScenarioContext. It is passed to `ScenarioStep\#execute` . But we need it whenever we create the `IMessage`. Currently, IScenarioContext is created in Builder. Steps are sometimes created earlier (when parsing a TestScenario file. Ideally we want the ScenarioStep to be as immutable as possible, but currently (with the classes and notions we have) we’re out of luck. Got to refactor or set the IScenarioContext somewhere.
Bluntly setting the IScenarioContext in BuilderPresenter works, but it’s a very poor approach prone to bugs and regression.
And it raised another question: what to bind the link to if the actual message is not received? I guess it worked fine and showed a message `_<Linked validation message is not yet available>_` It should have, I think.
IScenarioContext is not reactive yet to all the forms in the scenario. Although it is not that hard to do. Or, it could be, if the linking is recursive (field A links to field B, field B links to A, or through a field C, does not matter).
Storing a `IScenarioExecutionContext`in TestScenario seems the right thing to do. It’s TestScenario’s context finally! It’ll let IScenarioStep\#scenarioContext be a final property.
But what in case of a Single form, where we also need to bind to some property. Namely, Session properties. Maybe it should have a different name and idea: a context to bind to something. ILinkContext or something.
Then we’re having a `IScenarioExecutionContext` in IForm. Does not feel right. We could set the ScenarioExecutionContext (or LinkingContext) when creating a Form in scenario step:
```Java
@Override
    protected SchemaForm createForm() {
        SchemaForm outboundForm = getSession().createOutboundForm(messageType);
        outboundForm.setScenarioExecutionContext(executionContext);
        return outboundForm;
    }
```
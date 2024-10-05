---
Created: 2024-02-13T02:38
Updated: 2024-05-13T10:32
---
Define a project (so called “core”, or “API”) common both for the main (runnnable app) project and used by plugin implementations.
- [ ] Remove excessive dependencies in SessionBase class
    - [ ] `SessionBase\#getOutboundSessionMenu` should return a neutral object not bound to JavaFX, should not reference `StorageUtil`, `Files`, etc.
        
        `getOutboundSessionMenu` when replaced should return some sort of outbound message specification that will include: messageType (String), description (used in Builder action buttons, in Workspace), something else maybe. Should we replace all String messageType usages in favour of a typed MessageSpecification object (that’ll include this details associated with a messages of a particular type?). Maybe even an interface so that plugins could implement it.
        
        This MessageSpecification will definitely come in handy when we start to care about session versions, added and removed operations.
        
        Is it a MessageSpecification or an OperationSpecification? We have a Timer which is not an outbound nor an inbound message?
        
        [[Steps to refactor String messageTypes to a dedicated MessageSpecification class|Steps to refactor String messageTypes to a dedicated MessageSpecification class]]
        
        [[Refactoring ISession.getOutboundSessionMenu to not use MenuItem and FX classes|Refactoring ISession.getOutboundSessionMenu to not use MenuItem and FX classes]]
        
    - [ ] Should not implement `SessionBase\#getPlugin`. Method should be implemented in concrete Session classes.
    - [ ] What to do about `SchemaForm` dependency. It brings too many transitive deps. Seems like `createOutboundForm` can be easily refactored and moved out of `SessionBase`.
- [ ] Refactor ISession
    - [ ] `ISession\#getHost` should not call `ProjectService`. Maybe eliminate method altogther. Pass come “context” object that will reveal only needed resources. Could be set in some event handler method.
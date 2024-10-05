---
Created: 2024-01-06T16:37
Updated: 2024-02-27T19:21
---
Trying to upgrade Java to Open JDK

# A list of existing issues related to the upgrade

## UI

- [ ] KeepDividerPositionsSplitPaneSkin does no longer work. **TODO** Explain what we wanted it to solve.
- [x] Badge picker in New Session dialog is currently disabled.  
    Some custom skins must be re-implemented. They are commented out now.  
    
    ![[Notion 2/Attachments/Untitled 12.png|Untitled 12.png]]
    
    - BadgePickerBehaviour.java
    - BadgePickerSkin.java
    - CategoryChoiceBoxBehavior.java
    - CategoryChoiceBoxSkin.java
    
    In some of them, the main problem is `_BehaviorBase_` class being missing. In some classes there are usages of KeyBinding class or something related that can supposedly be replaced with the usage of inputMaps (see parent classes and relative skin/behavior implementations).
    
- [ ] In Runner, the checkbox used in the table to select test cases by their status is not aligned with the table header.
    
    ![[Notion 2/Attachments/Untitled 1 5.png|Untitled 1 5.png]]
    
    Java 8
    
    ![[Notion 2/Attachments/Untitled 2 3.png|Untitled 2 3.png]]
    
    Java 21
    
    ![[Notion 2/Attachments/Untitled 3 3.png|Untitled 3 3.png]]
    
    Java 21, no checkbox in the header
    
    ![[Notion 2/Attachments/Untitled 4 2.png|Untitled 4 2.png]]
    
    Java 8, Checkbox is present and clickable
    
- [ ] Overlay Scroll Bar in Scroll Pane

## Non-UI

- [ ] Can’t generate report when running a batch from CLI (See the page for details)
    
    [[ReportUtil problem related to XML Binding dependency]]
    

# Issues identified before the actual upgrade

- [ ] Some custom skins must be re-implemented. They are commented out now.
    
    - BadgePickerBehaviour.java
    - BadgePickerSkin.java
    - CategoryChoiceBoxBehavior.java
    - CategoryChoiceBoxSkin.java
    
    In some of them, the main problem is `_BehaviorBase_` class being missing. In some classes there are usages of KeyBinding class or something related that can supposedly be replaced with the usage of inputMaps (see parent classes and relative skin/behavior implementations).
    
- [ ] A few selector lookups should be checked. They may work fine, or may not.
    
    ```JavaScript
    MDICanvas.java
    MDICanvas()
                Node viewport = taskBar.lookup(".viewport");
    ApplicationLogPresenter.java
    initialize(URL, ResourceBundle)
                ScrollBar verticalBar = (ScrollBar) logTableView.lookup(".scroll-bar:vertical");
    ```
    
    But most of them are used in Modena sampler.
    
- [x] Finding IPlugin implementation classes is no longer possible with [Reflections library](https://github.com/ronmamo/reflections). A few issues report this: [https://github.com/ronmamo/reflections/issues/440](https://github.com/ronmamo/reflections/issues/440), [https://github.com/ronmamo/reflections/issues/377](https://github.com/ronmamo/reflections/issues/377).
    
    Check if this workaround works: [https://github.com/ronmamo/reflections/issues/373](https://github.com/ronmamo/reflections/issues/373). May need to update to version 0.10.2 of the library to check. Requires code changes.
    
    Other ways to solve this issue:
    
    - [ ] Use a different classpath scanning library like this one: [https://github.com/classgraph/classgraph](https://github.com/classgraph/classgraph)
    - [ ] Use [ServiceLoader](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) framework. Not sure, if we need to actually declare the implementing classes in a different JAR. If we can, we can define all of them in our main JAR (where the FX UI is). We’ll have to separate plugins in subprojects eventually anyway. Services can be declared using `module-info.java`.
- [x] In Builder, List tab (with scenario steps) is not created when a Scenario is opened. Also, scenario tab header is misaligned. Moving the divider between Scenarios list (on the left) and scenario tab helps. Only happens once after startup. If you try to open two scenarios, both of their tab headers are not visible.  
    Caused by faulty KeepDividerPositionsSplitPaneSkin that no longer works  
    
- [ ] JXBrowser causes a delay when closing the app. I think we’re blocking until all browsers are shutdown. Maybe do this in a background thread?
- [x] Problem with packaging: jpackage writes an exe file with read-only permissions. Can’t call `gradle clean` afterwards.
- [ ] Had to comment method. `se.suncom.multiq.ui.utils.UiUtils\#scrollToItemIfNotVisible` Restore it.

# Reasons for upgrading

- Building custom JRE images (smaller in size)
- Ease of writing code
    - Syntax changes
        - [JEP 286: Local-Variable Type Inference](https://openjdk.java.net/jeps/286)
        - [JEP 325: Switch Expressions (Preview)](https://openjdk.java.net/jeps/325)
        - [JEP 355: Text Blocks (Preview)](https://openjdk.java.net/jeps/355)
        - [JEP 359: Records (Preview)](https://openjdk.java.net/jeps/359)
        - [JEP 305: Pattern Matching for instanceof (Preview)](https://openjdk.java.net/jeps/305)
        - [JEP 406: Pattern Matching for switch (Preview)](https://openjdk.java.net/jeps/406)
        - [JEP 430: String Templates (Preview)](https://openjdk.java.net/jeps/430)
        - [JEP 443: Unnamed Patterns and Variables (Preview)](https://openjdk.java.net/jeps/443)
    - [JEP 358: Helpful NullPointerExceptions](https://openjdk.java.net/jeps/358)
    - [JEP 360: Sealed Classes (Preview)](https://openjdk.java.net/jeps/360)
- Related to plugin development
    - HTTP2
    - [TLS 1.3 (since Java 11)](https://openjdk.org/jeps/332)
- JavaFX related
    - Scale app UI on higher density displays. [JEP 263: HiDPI graphics: automatic scaling and sizing](https://openjdk.java.net/jeps/263)

Main reasons for upgrading Java are the following:

- Some libraries drop Java 8 support and compile for newer version of bytecode than Java 8 supports and may also use classes/methods from a newer SDK. Hence they can’t be used on Java 8. However we can use libraries compiled for Java 8 (Unless using a feature later removed, a rare occurrence with Java). I remember I had to recompile a lib to use with our project.
- Bugs are fixed in JDK and in JavaFX. None that we majorly affected us though.
- Features particularly interesting for our app:
    - JavaFX related
        - Java can scale app UI on higher density displays. Like when we’re using UI scaling on Windows, for example. Currently, the app has the same size in pixels no matter what scaling is set in Windows. [JEP 263: HiDPI graphics: automatic scaling and sizing](https://openjdk.java.net/jeps/263)
        - We can package our app with a custom JRE and strip some unused modules to make distribution size slightly smaller.
        - We can use a newer version of ScenicView (a tool pretty much like an Inspector panel in a browser). v8 had a couple of bugs. It loses connection to the main program sometimes. Although I am not sure if it will work the latest version of JDK smoothly. Need to check.
        - Reactive Streams (introduced in Java 9) for concurrency?
    - Related to plugin development
        - HTTP2
        - [TLS 1.3 (since Java 11)](https://openjdk.org/jeps/332)
- Better syntax, better standard library, more useful methods available on already known classes. It makes coding more enjoyable and the code is expressive.

Java 8 was released almost 10 years ago in March, 2014. I am considering the transition to a newer Java version to be inevitable.
---
Created: 2023-11-11T00:37
Updated: 2024-03-08T14:14
---
Licensing, keys and protection
Ways to protect java code
Packaging
Updates
Building
Logging
Release notes
Versioning
Dialogs
Discussed with Vasilis
# Licensing, keys and protection
Obfuscation is not worth it. The software will not be available for public. We can get away with something basic like License3j for now.
- [ ] Search for third-party licensing libraries and servers, even for different platforms. Based on the gathered information make a list of features that we might be interested in.
- [ ] Write a list of issues we may run into when making a licensing stuff for a program written in Java particularly.
#### Licensing software
|Name|Features|URL|OSS|Comments|
|---|---|---|---|---|
|[[LicenseSpring\|LicenseSpring]]||[https://licensespring.com](https://licensespring.com)|[ ]||
|[[License3j\|License3j]]||[https://github.com/verhas/License3j](https://github.com/verhas/License3j)|[x]|Apache 2.0 license, version 3 and later are only for Java 11, but will work on Java 8, because bytecode is compatible ???|
|[[Notion/IntelliQ/Github Issues/Licensing, keys and getting ready to ship to the customers/Licensing software/Untitled\|Untitled]]|||[ ]||
  
  
## Ways to protect java code

> [!info] Беззащитная Java. Ломаем Java bytecode encryption  
> Код на Java не так прост, как кажется.  
> [https://xakep.ru/2022/04/26/java-bytecode-encryption/](https://xakep.ru/2022/04/26/java-bytecode-encryption/)  
# Packaging
Requirements:
- Possible to use on Java 8 to 21.
- Should bundle JRE
- Target Windows, Linux, Mac
`javapackager` is removed in Java 9. [jpackager](https://openjdk.org/jeps/392) is introduced in 14 as an incubating feature.
#### Packaging software
|Name|Features|URL|OSS|Comments|Compatibility|
|---|---|---|---|---|---|
|[[launch4j\|launch4j]]|Bunde JRE, Signing|[https://launch4j.sourceforge.net](https://launch4j.sourceforge.net)|[x]|Can it bundle a JRE?||
|[[install4j\|install4j]]|Automatic Updates, Bunde JRE, Custom Installer Views, Enforce single instance on Windows, GUI Editor, Signing, i18n|[https://www.ej-technologies.com/products/install4j/features.html](https://www.ej-technologies.com/products/install4j/features.html)|[ ]|Advanced GUI editor, can install services  <br>  <br>Expensive: €1869 Multi-Platform Edition|Java 8 - latest|
|[[javapackager\|javapackager]]|||[ ]||Up to Java 8|
|[[jpackage\|jpackage]]|||[ ]||Java 14 - present|
|[[Advanced Installer\|Advanced Installer]]||[https://www.advancedinstaller.com/user-guide/native-java-launcher.html](https://www.advancedinstaller.com/user-guide/native-java-launcher.html)|[ ]|||
|[[izpack\|izpack]]|Cross compilation|[http://izpack.org/](http://izpack.org/)|[x]|Can install “packages” (could be used by us for plugins)|< Java 8?|
|[[InstallShield\|InstallShield]]|||[ ]|||
|[[NSIS\|NSIS]]|||[x]|Simple, exensible by plugins||
|[[Conveyor\|Conveyor]]||[https://www.hydraulic.dev/blog/1-hello.html](https://www.hydraulic.dev/blog/1-hello.html)|[ ]|||
  
  

> [!info] picocli - a mighty tiny command line interface  
>  
> [https://picocli.info/#_packaging_your_application](https://picocli.info/#_packaging_your_application)  
Picocli suggestions on launchers, mainly.

> [!info] Install Designer  
> Powerful and user friendly tool for creating NSIS and Inno Setup dialogs (setup Forms and Pages) without any scripting.  
> [http://www.install-designer.com/](http://www.install-designer.com/)  
# Updates
No need to provide automatic updating mechanism. Distributions will be available on our website for download.
# Building
We will provide different application builds for each client. Different in a set of plugins. Some will be include for a particular client, some will not be. But before this we should separate plugins code from the application code into separate projects. Workaround is also possible: hide (disable) plugins.
- [ ] Come up with a list of general directions on how to split the project into modules
    
    - [ ] Define what classes should constitute the “core” of the application.
        
        What is a core? Since we have a requirement of a CLI interface, the core should probably provide the same functionality as the full-blown JavaFX GUI application when adapted properly. It should be adaptable to a CLI interface and retain all the basic functions like:
        
        - Running a single scenario (optional, really). We can’t at the moment.
        - Running a batch
        
        That’s probably it, other things (creating sessions, creating scenarios) would be cumbersome to do without a normal GUI.
        
        Ideally, we should be able to run a batch without using any JavaFX classes, because we don’t need the GUI. And it should also be easier to test the application.
        
        We’re not yet looking to adopt a different application architecture (like MVVM) here. Just taking plugin code out of the main application.
        
    - [ ] Is it possible to keep the dependency of plugin classes on JavaFX library? To do less restructuring.
    
    - Reading materials
        
        > [!info] Dependency inversion principle  
        > In object-oriented design, the dependency inversion principle is a specific methodology for loosely coupled software modules.  
        > [https://en.wikipedia.org/wiki/Dependency_inversion_principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)  
        
        > [!info] Refactoring Module Dependencies  
        > An example of taking a program, splitting it into modules by layers, and refactoring these dependencies with the Service Locator and Dependency Injection patterns.  
        > [https://martinfowler.com/articles/refactoring-dependencies.html](https://martinfowler.com/articles/refactoring-dependencies.html)  
        
    
    More tasks to follow?
    
CI, CD. Problem: with every version (major or bugfix) we need to build the application for several (in future) customers and platforms (Linux, Windows). Ok, be it a single platform, it is still a problem. Then we need to store built artifacts somewhere. This should be done on a remote server. What tasks should I define now for this matter? Is it urgent? I guess, not.
  
# Logging
We need a convenient way to collect logs, but there’s no need to send them automatically from within the application, because Internet may not be available. So, we need to provide a way just to point a user to the logs or attach them to the Email program like Outlook.
Get the logs. Mail them. Attach logs automatically. Or just download.
**Don’t show exception stacktraces. Soon.**
Error ids?
# Release notes
# Versioning
## Dialogs
We should probably use a decent Dialogs library instead of what we have now. It’s a pain to use them.
The one from GemsFX, probably. JFoenix also offers something.
https://github.com/dlsc-software-consulting-gmbh/GemsFX
- [ ] Create an issue to replace dialogs
    - [ ] Create a few examples, why it is going to be better and more clear for us, developers
    - [ ] Find existing issues with Dialogs. If I am not mistaking, there was an NPE thrown when the root pane was not a StackPane. Maybe it’s the case when using Viewer in a separate Window.
## Discussed with Vasilis
- [ ] OpenAPI definition might need to be changed later, as the API develops. How are going to handle this? Create new sessions, change settings of existing sessions? What if some methods are removed? What if some methods are modified: parameters, return types, properties in return types?
    
    Let’s imagine, settings are changed for an OpenAPI session. A different definition is imported, meaning: new outgoing message types and new incoming message types. Messages can have different structure now. And saved forms too (both validation forms with expected values and actual forms).
    
    How do we resolve these differences? We want to keep scenarios, otherwise we would not even offer an option to change a spec for the session, the user would only be able to create a new session, meaning all scenarios would become obsolete.
    
    We’re going to offer the user two options: try to patch the existing project or disable changed/removed operations in scenarios.
    
    - **Disabling**. Used messageTypes (should we call ‘em operations, use a class instead of raw String) that are missing in the new spec, used message types that has changed will be marked as disabled (grayed out, invalid). You will not be able to run such a scenario without replacing these scenario steps. Replacing meaning manually deleting and adding from Actions panel again.
    - **Patching**. Ok, so some of the items are missing in the new spec. Disable them. But some have changed. We want to keep some data in the scenario steps. In order to do so, we should:
        - Match operations. By message type, or something protocol specific. Need to think about it.
        - Patch scenario steps. If some parts of message (form) structure matches, copy such part from the old (existing) scenario step.
    
    What to do with messages serialized from Viewer? Let’s explore this idea. We don’t have to implement the same elaborate mechanism for Viewer and try to load messages from an earlier version of spec. But it may bring useful ideas.
    
- [ ] Same for FIX
    - [ ] How FIX is customized at all?
- [ ] Regex feature. A template “Contains x”. What if we want to check if the actual contains a certain string? How are we going to store this template: as a single string (and then parse it to check if it is a “Contains X” expression) and show appropriately or store as structure: `{template: “Contains”, “args”: [”x”]}` ?
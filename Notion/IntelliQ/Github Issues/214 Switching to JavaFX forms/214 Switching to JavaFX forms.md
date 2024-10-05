---
Created: 2024-04-15T20:26
"Issue #": 214
Updated: 2024-08-21T14:18
---
Features
Related features of the application that may be impacted
Search and Replace
Form templates
Linking
Implementation
Challenges:
Libraries to use/look at:
Types
Wrapping up
Ongoing notes
21.08 Multiline validation labels
# Features
Current features:
- Form validation
    - Validate the whole form on Submit
    - Clear the form
- Required (`*`) mark on form field
- Currently supported field types:
    - Enum dropdowns. A set of values is provided (numeric) and string descriptions of these values
    - String inputs
        - date
        - date-time
    - Number inputs with spinner buttons
        - multipleOf
    - Nested objects
    - Arrays of objects
    - Pretty much any validation constraint can potentially be used in OpenAPI session, because any OpenAPI definition can be used.
- Field links
- Search and Replace on form (step) data
- Dirty tracking on forms: if the value in the form is changed, mark the scenario in Builder as dirty
What may we want to customize during **runtime** (customization by the end user, config files, etc)? Currently, only form titles are customized.
# Related features of the application that may be impacted
## Search and Replace
We’re operating on the JSON model of forms in the current implementation of Search and Replace. We use `IForm\#setModel` to update the model (values of fields).
## Form templates
Saving and loading form templates. The form data (the `model`) is stored as JSON.
## Linking
![[Untitled 11.png|Untitled 11.png]]
  
  
`FieldLink` class and descendants may be affected
# Implementation
## Challenges:
- Json Schema can be recursive (with `$ref`s). Swagger lib allows to inline such refs
- OpenAPI JSON Schema format is a little bit different than the standard one (extra properties are used).
- We **have** to be able to convert any OpenAPI schema to a form. Challenge is to process this schema properly, care about all the edge cases. Do we need an intermediary structure between a Schema class and the JavaFX controls? Some kind of a definition that other protocols could use directly (instead of using either JavaFX controls or a Schema class).
- Polymorphism in Open API Schemas.
- Form data should be serializable into a JSON for further retrieval by a Session implementation. We could use Visitor pattern to walk the form and create a JSON document.
  
What is the purpose of “PropertyDefinitions”? Or form definitions? It can be used to link something with a property without the existence of a Form or actual values of such property.
## Libraries to use/look at:
https://github.com/dlsc-software-consulting-gmbh/FormsFX

> [!info] Forms  
> Lightweight JavaFX Framework for Kotlin.  
> [https://github.com/edvin/tornadofx/wiki/Forms](https://github.com/edvin/tornadofx/wiki/Forms)  
https://github.com/dooApp/FXForm2

> [!info] Bitbucket  
>  
> [https://bitbucket.org/zuunr/json/src/master/](https://bitbucket.org/zuunr/json/src/master/)  
https://github.com/Hanseter/JSONPropertyEditorFx
https://github.com/Hanseter/JSONPropertyEditorFx
https://github.com/apache/commons-validator
## Types
Entities:
# Wrapping up
Pros for switching to JavaFX:
- Adding more functionality to the forms would be easier because we would not have to use JavaScript and could reuse JavaFX components.
    - Useful controls (I will demonstrate on request):
        - ControlsFX → TextFields → Autocomplete
        - ControlsFX → Searchable ComboBox
        - GemsFX → Time Picker
    
- Consistent styling with the rest of the application. Control styles are used by forms too.
- Native feel and behavior of controls. See for example how datetime picker or dropdown is implemented. You can set the dropdown to be used with a custom (user provided value), but there’s a JavaFX control just for this:
    
    ![[Untitled 1 4.png|Untitled 1 4.png]]
    
- JXBrowser requires Chromium running in a separate process. It’s a potential source of problems. We did not have any with the latest version, but with the one we used previously there were:
    - different UI scaling in forms and in the rest of the app
    - JXBrowser’s thread prevented app from exiting
Cons:
Problems:
- I still can’t use the license (30 days trial) on my machine. Gotta run the app from a VM I guess.
If the application is ever going to be used in a real environment, we should switch to JavaFX sooner or later.
# Ongoing notes
## 21.08 Multiline validation labels
We want this:
![[image.png|image.png]]
But the scroll pane prevents us. When the scroll bar is visible the label is set to its min Height:
![[image 1.png|image 1.png]]
If we set min Height manually, say to 50, it becomes multi-line. This minHeight seems to be computed here: `javafx.scene.control.skin.LabeledSkinBase\#computeMinLabeledPartHeight`,
`com.sun.javafx.scene.control.skin.Utils\#computeTextHeight(javafx.scene.text.Font, java.lang.String, double, double, javafx.scene.text.TextBoundsType)`.
Если FormControl наследовать от ScrollPane и прямиком туда setContent, получаем такой вот глюк. Окно слева. Обрезаны контролы с правой стороны.
![[image 2.png|image 2.png]]
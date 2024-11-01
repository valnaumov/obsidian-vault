ChatGPT on this topic: https://chatgpt.com/c/67179f82-c6b4-8007-bbb8-649fe8e43678
What I want:
- Link any field to any field
- Link outbound form fields to validation forms and vice versa
- Link any form to session parameter
- Show an overlay above textfield controls (including sub-elements of the controls like spinner editor).
- Prevent linking loops
- Should be able to see the actual value of link when hovering the editor
What to keep in mind and take care of, possible pitfalls:
- Steps (forms) can be removed from a scenario. We should do something about the links the point to this form. Have a dispose method on Form?
- Need to notify subscribers of Session Parameter changes somehow.
	- ParameterItem is a class of its own. We can use interfaces and bind to `ParameterItem#value` changes.
- If we want to be able to link a number to a string field, we should take care of cases when a string becomes **unconvertable to a number** (was "1.01", but became ".001", for example). Should link be disabled temporarily or permanently? Should probably not implement this and link to the same type at first.
- If linking is not possible, we should show an appropriate **error message**.
- **Search and Replace** should be able to replace links. Or not? Ask Vasilis

Ideas:
- Apache Commons has a converter class supporting conversions between common JDK types.
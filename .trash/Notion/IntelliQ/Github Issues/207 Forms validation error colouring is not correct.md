---
Created: 2023-12-06T16:58
"Issue #": 207
Updated: 2023-12-18T23:28
---
What I wanted from Elias:

> [@elibon99](https://github.com/elibon99)  
> Also, clearing ClOrdId and hitting Send does not highlight this field  
> as invalid although it's a required field. FYI, the field is empty in  
> form data in this case (which is ok, meaning it's actually empty).  
> 
> SchemaForm thinks that since a field value is not null (although being an empty string), it should pass. Where else can we apply a workaround? ui schema? Field class?

  

1. Required fields in nested objects are not validated at all (master branch).
    - [ ] Add an example: how to test
2. In addPetToOwner form nothing no validation errors are shown even if all of its fields are empty.
    1. `path.ownerId` - integer, but no error when blank
    2. `body.bithDate` - not validated, that’s known, birthDate is of type `string` .
    3. `body.name` - not validated, same
        1. `body.type.id` - not validated although id type is `integer`
        2. `body.type.name` - not validated, `string` type
3. No validation error text is shown in the form. It can be quite confusing. For example, in NewOrderSingle form has OrderQty field set to be a `multipleOf": 100"` When we OrderQty to 150 and hit enter, we get red validation error coloring around OrderQty field, but we don’t know what caused it. It’s filled, but is not valid for some reason.

  

TODO:

- [ ] Create a separate method in a Utility class (for testability). But it could be a static method as well.

Problem with validation of nested objects:

```JavaScript
path": {
      "properties": {
        "ownerId": {
          "minimum": 0,
          "exclusiveMinimum": false, // here
          "type": "integer",
          "types": [
            "integer"
          ]
        }
      },
      "type": "object",
      "required": [
        "ownerId"
      ]
    },
```

`exclusiveMinimum` must be a number according to [JSON Schema](https://json-schema.org/draft-06/json-schema-validation#rfc.section.6.5). But we bluntly serialize `Schema` only excluding a few properties, so it is not exactly compatible. And there may be even more problems.
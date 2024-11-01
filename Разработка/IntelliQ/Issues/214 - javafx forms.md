# allOf combination
allOf используется, как я понимаю, в основном для реализации наследования, как в этом [примере](https://swagger.io/docs/specification/v3_0/data-models/oneof-anyof-allof-not/#allof) на сайте Swagger. Там нужно обратить внимание на Pet и "наследников" Cat и Dog.
Когда оба элемента allOf - объекты, всё просто. Совмещаем все свойства обоих объектов в один объект. Как бы просто.
Сложности возникают, когда у объектов разные типы: например, number - string, string - array, array - object и так далее.
Думаю, есть смысл ориентироваться на [react-json-schema](https://rjsf-team.github.io/react-jsonschema-form/).
react-json-schema не показывает UI, когда типы пропертей не пересекаются. Допустимых типов пропертей может быть несколько, они могут пересекаться, чего я не учёл (возможно, и не нужно, пока):
```json
{
  "type": "object",
  "allOf": [
    {
      "properties": {
        "lorem": {
          "type": [
            "string",
            "boolean"
          ],
          "default": true
        }
      }
    },
    {
      "properties": {
        "lorem": {
          "type": "boolean"
        },
        "ipsum": {
          "type": "string"
        }
      }
    }
  ]
}
```
На примере выше lorem в одной схеме может быть string и boolean, а в другой — только boolean. Соответственно, форма показывает чекбокс только для boolean. Если бы было string, boolean и string, форма показала бы только text field для string.
Самый забористый вариант — когда учитываются даже enum.
```json
{
  "type": "object",
  "allOf": [
    {
      "properties": {
        "lorem": {
          "type": "array",
          "title": "A list of strings",
          "items": {
            "type": "string",
            "default": "bazinga",
            "enum": [
              "foo",
              "bar",
              "fuzz"
            ]
          }
        }
      }
    },
    {
      "properties": {
        "lorem": {
          "type": "array",
          "title": "A list of strings",
          "items": {
            "type": "string",
            "default": "bazinga",
            "enum": [
              "foo",
              "bar",
              "sdsd"
            ]
          }
        }
      }
    },
    {
      "properties": {
        "lorem": {
          "type": "array",
          "title": "A multiple choices list",
          "items": {
            "type": "string",
            "enum": [
              "foo",
              "bar",
              "fuz",
              "qux"
            ]
          },
          "uniqueItems": true
        },
        "ipsum": {
          "type": "string"
        }
      }
    }
  ]
}
```
На примере выше три схемы, в комбинации allOf, в каждой есть пропреть lorem, у неё везде тип array, а тип элементов массива — везде string. Однако различаются они enum'ами внутри.
react-json-schema показывает select, где можно выбрать несколько элементов, перечисленных в enum (то, что мы могли у себя показать, используя ChoiceBox). Такой контрол, видимо, выбран, т.к. `uniqueItems`. Но главное, он **показывает доступными для выбора enum'ы общие для всех схем.**
Короче, тут какая-то серьёзная логика в сравнении схем, и нахождении "общей схемы". Нужно ли её реализовывать и как?
У меня сейчас не учитываются required на combined properties. Если хотя бы в одной схеме из набора allOf есть required, то в combined оно тоже должно быть помечено как required.
# Linking
[[Linking with JavaFX forms]] 
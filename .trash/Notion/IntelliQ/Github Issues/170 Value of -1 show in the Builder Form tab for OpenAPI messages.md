---
Created: 2023-02-10T00:06
Updated: 2023-03-03T17:39
---
- Как показать Actual и Expected в одном TreeView?
    
    Нужно делать по аналогии с `JsonTreeItem` , только будем итерировать всегда два объекта одновременно (expected, actual).
    
- Как будем показывать Actual и Expected, если объекты разных типов?
    
    Например:
    
    ```JSON
    {
      "glossary": {
        "title": "example glossary",
        "GlossDiv": {
          "GlossList": {
            "GlossEntry": "hey",
            "GlossEntry2": "lol"
          }
        }
      }
    }
    ```
    
    ```JSON
    {
      "glossary": {
        "title": "example glossary",
        "GlossDiv": [
          "this is a literal",
          {
            "key": "value"
          }
        ]
      }
    }
    ```
    
    |   |   |   |
    |---|---|---|
    |expected|actual||
    |object|array|Можно показывать элементы массива по индексу, поля объекта — по их именам|
    |primitive|array|элементы массива я показываю со следующей строки как вложенные, а вот на той же строке, где имя элемента, можно показать значение примитива|
    |primitive|object|так же, как и в прошлом случае|
    

А ещё нужно будет сделать редактирование в ValidationForm.

# TreeTableView

Требования:

- При редактировании элемента ноды в таблице не закрываются и не открываются. Остаются так же. Пишу об этом, т.к. `TreeTabelView\#refresh` может повлиять.

Для чего я использую JsonPair, если можно в нашем кастомном классе `JsonPairTreeItem` указать оба поля сразу. Также удобно указать имя проперти в `JsonPairTreeItem` , чтобы не обращаться каждый раз к родителю, ведь у нас уже есть родитель, когда мы создаём детей.

Хотелось бы сохранить возможность фильтрации (как в `RecursiveTreeItem` уже сделано).

Cейчас нужно добавить редактирование дерева, а я не понимаю, как это должно работать, и как должны вести себя actual и expected элементы, что будет в JsonPair. Нужно это проработать, визуализировать. Сейчас занимаюсь гаданиями.

### JsonPair: subclassing vs flat

Какая функциональность нужна в ValidationFormPresenter?

- `clearAllValidations` — то есть вcе JsonPrimitive заменить в своих родителях на null. Но не удалить.
- `applyVerifyAllFieldsTemplate` — JsonPrimitive ноды заменить
- `setExpectedValue` на JsonPair, где expectedValue — primitive. Типа
    
    ```Java
    onShowLinkToParameter.accept(param -> primitiveItem.setExpectedValue(param.getLinkString()));
    ```
    
- `getIndex`
- `getPropertyName`

На Array:

- `append`
    - object
    - array
    - primitive

На Object:

- `append`
    - object
    - array
    - primitive

И то же с `insert`

```JSON
if (expected == null || actual == null
            || !expected.getClass().equals(actual.getClass())) {
```

Условие `!expected.getClass().equals(actual.getClass()))` реально выполняется когда-нибудь?

Да, выполняется. Объекты разных типов могут быть на одной ноде. Например, по индексу или ключу:

```Java
for (String key : allKeys) {
    children.add(childOf(left.get(key), right.get(key)));
}
```

Поэтому, если и будет какой-то subclassing, то на основе parent-типа.

Почему нельзя помимо прочих типов: JsonObjectPair, JsonArrayPair, JsonPrimitivePair ввести ещё такой тип, когда объекты разные JsonElementPair. Методы, которые проверяют тип объекта, необязательно должны возвращать Optional. Так получится какое-то общее поведение определить, а заодно явно обозначить, какие варианты JsonPair бывают, и соответствующую реализацию методов рядом.

А если один из элементов Null, какую реализацию создавать? А как быть, если устанавливают какое-то значение в такой смешанный тип JsonElementPair? Тип-то уже не поменяешь, будет несоответствие! Однако, во всех случаях, когда мы задаём expectedValue на JsonPrimitivePair, нам нужно заменять элемент в родителе. Вот тут-то и можно создать новый JsonPair, вызвав initChildren на родителе.

Окей, а наличие такого смешанного типа JsonElementPair вообще упростит мне работу? Потому что что-то придётся проверять в любом случае. Например, может ли expectedElement в этой JsonPair иметь propertyName, index и т.д. Это можно обойти, если создавать JsonPrimitivePair или JsonObjectPair и т.п. такую, как бaы синтетическую. Где один элемент будет null. Но тогда в настоящей должна быть проверка в конструкторе: нельзя разрешать там null-элемены. Но это только для тех сущностей, где один из (expected или actual) равен null.

Если мы такой же подход применяем в том случае, когда объекты разных типов, можем выбрать только один. Что тогда? Методы asObject, asPrimitive, asArray нужны будут для того, чтобы добавлять/удалять ноды. А что касается колонки Name, то оба объекта добавляются в JsonPair по имени или индексу.
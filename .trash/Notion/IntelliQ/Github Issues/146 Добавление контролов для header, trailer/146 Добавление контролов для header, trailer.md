---
Created: 2022-01-09T23:00
Updated: 2022-03-01T01:04
---
Два экстремальных варианта:

Всё нетипизированное:  
IMessage  
header  
trailer  
body  
generalInfo  

Плюсы:

- не нужно конвертировать в JSON, когда это требуется, т.е. при:
    - сохранении
    - замещении ссылок (${parameter}).
    - загрузке
- сообщение уже разделено на секции. Но это чисто структурное преимущество: protocolMessage тоже разделяется (мы выделяем из него хедеры, тело и пр.), просто в другом месте.

Минусы:

- в StepMessageView нельзя сразу получить protocolMessage и создать нужные контролы.  
    К примеру, в ValidationMessage view нельзя будет HttpResponse.getStatusLine().getStatusCode(). Вместо этого придётся конвертировать всё, что есть в IMessage (header, protocol, body, generalInfo) в protocolMessage и из него получать status code. Ну или знать, в каком поле в general info он лежит.  
    

Другой вариант (не экстремальный, на самом деле).  
Храним IMessage.protocolMessage. Извлекаем и устанавливаем обратно header, trailer, body, general по мере необходимости из protocolMessage.  

Когда необходимо их извлекать?

- Для показа в StepMessageView
- Для замены в IScenarioExecutionContext\#updateModelWithVarValues

Когда необходимо устанавливать обратно?

- После редактирования в StepMessageView
- После замены в IScenarioExecutionContext\#updateModelWithVarValues

Как устанавливать обратно?  
Создавая новое protocolMessage: ISession\#createProtocolMessage  

Как будут выглядеть сигнатуры для получения headers из protocolMessage?  
Map<String, String> ISession.getHeaders(IMessage)  

Как будут выглядеть сигнатуры для создания IMessage по headers, trailer?  
ISession\#createInboundMessage(message, header,trailer,body(form model))  
ISession\#createOutboundMessage(message, header,trailer,body(form model))  

**Где будут методы isHeaderSupported, isTrailerSupported, isBodySupported?**  
Созданное сообщение может и не иметь этих полей. Следовательно, спрашивать нужно сессию. Т.е. добавляем методы в сессию. Потом эти методы можно объединить с ISession\#getFormDefinition, ISession\#getJsonSchema в некий MessageTypeSpecification или просто MessageSpecification.  

```Java
boolean isHeaderSupported(String messageType);
boolean isBodySupported(String messageType);
boolean isTrailerSupported(String messageType);
Map<String, String> getHeader(IMessage message);
Map<String, String> getTrailer(IMessage message);
```

`getBody` не имеет смысла. Не клеится всё как-то. Что если будут классы, реализующие IMessage, но специфичные для каждого плагина?

Хранить не типизированные поля сообщения плохо ещё с такой стороны. Когда мы получаем сообщение, мы преобразуем его поля в JSON (и мапы). Затем мы можем показать это сообщение во Viewer, где оно будет отформатировано. Для этого нам понадобится опять преобразовать в protocolMessage.

В случае с сообщениями в Builder, которые в данный момент генерируются в SendMessageScenarioStep: сообщение генерируется каждый раз, когда меняется форма.

Уже в конце, при сохранении на диск, нам удобно иметь сообщение в виде JSON.

Хорошо бы перейти на Jackson полностью.

Возможно, также удачно будет использовать JsonNode (например, от Jackson) как тип header и trailer вместо мапы. Потому что нет гарантий, что header не будет иметь древовидную структуру. Кроме того, поля JSON-объекта - типизированные. А в случае с Jackson’ом, там ещё и разные подтипы Number возможны. Впрочем, всё равно надо почитать статью, как создавать объекты в Jackson’е.

IForm\#getX, `getHeigh` `IForm\#boundsProperty`, в `se.suncom.multiq.interfaces.impl.SessionBase\#getOutboundSessionMenu` в действительность — не свойства формы, а некой сущности DesktopWindow. Форма — это нечто для редактирования тела сообщения. Это единственный способ редактирования, но только пока. Для HTTP-плагина можно будет добавить JSON, XML редакторы — это не очень сложно, но полезно. Или даже не несколько редакторов, а текстовый редактор с поддержкой разного форматирования.

И ещё раз надо поставить задачу.

# Задача

Задача: для показа пользователю, логически разделить сообщение в UI на headers, body и trailer. И какую-то общую информацию. Body сообщения может быть не только формой (form model, как мы сейчас разбираем), но и просто строкой. Поэтому мы не можем просто использовать то же представление в виде JSON для ShemaForm, что и для сохранения на диск.

Но на диск мы тоже сохраняем в JSON. А когда восстанавливаем, передаём это методам ISession\#createMessage... И сохраняем мы сейчас формы, а не сообщения.

Короче, итог размышлений такой: не обязательно сохранять то, что нам возвращает getMessageBody. Для сохранения можно предусмотреть другой метод.

# Проблемы сейчас

- [ ] FieldLink использует IMessage\#toJson, из message, который он получает от MessageScenarioStep\#getExpected
    
    У нас происходит конвертация (header, body, trailer) → IMessage → json. К последнему надо как-то применить json Path из FieldLink, поменять его формат.
    
    Придётся менять ещё и JavaScript code.
    
- [ ] Как передавать данные для MessageValidator?
    
    Оба как message или как header/body/trailer для expected и actual — это 6 параметров. В ValidationView от контроллов мы получаем JSON, только потом он может быть, если есть необходимость, сконвертирован в IMessage. Не хочется делать лишние конвертации. Какие ещё аргументы против того, чтобы передавать в MessageValidator IMessage? Нельзя использовать в качестве expected инстанс IMessage, потому что пустые поля в form model означают, что их нужно игнорировать во время валидации. А IMessage может содержать и некоторые генерируемые поля (которые, не нужно сравнивать).
    
- [ ] Что передавать в конструктор(ы) MessageScenarioStep? JSON’ы или IMessage?
- [x] `se.suncom.multiq.interfaces.ISession\#isFormSupported` должен называться так или `isBodySupported`? Есть ли разница в смысле?
- [x] Message body — не обязательно JSON. Что если это plain text или XML? Как в таком случае валидировать их? Как преобразовывать в JSON для показа во View? Нужно ли это делать? Как валидировать? Допустим, пришёл plain text, его не завалидируешь с помощью ValidationForm. Нужно какой-то другой view. **Плагин должен выбирать View.**
    
    Для случаев, когда тело сообщения — не JSON, нужно использовать другой SendMessageView, который не основан на SchemaView. Потому и не должно быть метода `ISession\#getMessageBody`, вместо него есть метод `ISession\#getFormModel` .
    

Есть ещё случаи, когда нужно представить сообщение в виде JSON:

- Для показа в TreeView в Builder или Viewer.
    
    Это весьма произвольно. Header, body, trailer. Если body можно представить как JSON (form Model), показываем. Если это XML или YAML (древовидная структура), тоже показываем. Если в теле просто строка, так и показываем `body: "Lorem ipsum"`.
    
- Для сохранения на диск
    
    Схоже с пунктом выше. Для этих двух случаев сейчас и так используется IMessageFormatter.
    
- Для получения значения определённого поля в сообщении с помощью FieldLink
    
    В этом случае проверять, можно ли представить тело сообщения в виде формы. Если можно, получать поле, которое в ссылке. Если нет, выдавать ошибку. Как поступать с заголовком и окончанием сообщения? Их можно связывать, несмотря на то, что тело сообщения нельзя представить как formModel.
    

# Как можно обойтись без разделения IMessage на header, body и trailer?

Как обойтись без этого разделения на уровне кода? Не для всех плагинов оно нужно. Как через плагин этим управлять?

Основное предназначение такого разделения: показ пользователю. Отдельно таблица для валидации header’а, отдельно для тела. И, может, когда-нибудь для трейлера.

На что влияет разделение?

- Сообщения об ошибках валидации. `header.content-type: Expected <application/json>, but was <application/xml>`
    
    _Это несущественно_ ✅
    
- Путь к полю в SearchAndReplacePanel ✅
- На то, как будет сохраняться сообщение на диск
    
    Плагин должен сам парсить и сохранять свои сообщения. Обработает все кастомные поля как надо.
    
- Представление в FormTabsPresenter

Итак, если отказываемся от разделения на header, body, trailer и т.д., то и в `LinkToSendMessageStepView` будет всё в виде дерева и текста. И в LinkToValidateMessageStepPresenter тоже.

Кто создаёт IMessage: `IMessageStepView` или `MessageScenarioStep`?

Какие вообще обязанности у классов?

- `IMessageStepView` позволяет создавать кастомный UI разработчику плагина. Может содержать в себе IForm, любые кастомные контроллы.
- `MessageScenarioStep` реализует логику работы шага в сценарии: что делается. Отправляется сообщение, валидируется, таймер.

Из ValidationForm/`IValidateMessageStepView` мы не можем получить сообщение, потому что по сути это лишь произвольная модель (дерево из ValidationItem), которая не представляет цельное сообщение (например, в настоящем сообщении может быть timestamp его создания, версия протокола, хэш, ещё что-то личное), а только поля, которые нужно валидировать. Это, конечно, не мешает нам получать из `ISendMessageStepView`IMessage, а из `IValidateMessageStepView` — ValidationItem. Если будет нужда создавать IMessage прямо в

`ISendMessageStepView` , то так и поступим, но пока в этом нужды нет.v

# Нужны ли вообще кастомные View или можно (было) обойтись SchemaForm?

Такой вопрос возникает оттого, что _по-видимому_, нас не особо интересует техническая часть. А именно, какие поля в хэдере будут переданы и т.п. К примеру, в GET-запросе id пишется как URL path variable, а тот же Swagger предоставляет форму (тут думаем про наши SchemaForm):

![[Notion 2/Attachments/Untitled 10.png|Untitled 10.png]]

Т.е. мы могли бы абстрагироваться от всех этих деталей, показывать SchemaForm, а плагин бы уже решал, куда эти заполненные поля подставлять. И хранили бы IForm\#getModel. Вроде просто.

Но:

- Точно хотелось бы видеть глагол запроса: GET, POST, PUT
- Хоть где-нибудь — URL. Хотя это можно и в форматтере показать. (Tree, Plain Text, вот это всё).

И вместе с тем:

- Неясно, куда спрятать:
    
    - `ISession\#getFormDefinition`
    - `ISession\#getJsonSchema` - это нужно и для SchemaForm, и для ValidationForm.
    - `getMessageFieldEnumValue` - закодированные значения некоторых полей формы
    - `getMessageFieldEnums` - то, как эти поля отображаются
    - `getMessageTypeFields` - Все поля (но, видимо, только верхнего уровня), которые поддерживает схема. Используется в ValidationForm
    
    Можно оставить там же, ведь в основном это будет использоваться (в Swagger, но не в простом HTTP-плагине, возможно. Если это будут разные плагины).
    
- Если вид — необязательно “форма”.
- Что теперь IForm?

Можно не отказываться от всех этих классов view, которые мы создали. Ведь TimerView у нас тоже будет. Ну и надо уже определиться, валидируем мы форму или сообщение.

  

  

Hi, Bill! Are we looking at the messages from the protocol perspective or from functional perspective? For instance, we can show just a form like we do now. We will generate it from OpenAPI definition [https://petstore.swagger.io/#/pet/updatePet](https://petstore.swagger.io/#/pet/updatePet). If we show just form, it means we’re going to hide implementation details like: specific headers used in the request, url, HTTP, etc. I think we should show this information somewhere. We could show it in Tree and Raw, which are actually OK in the beginning.

So, back to my question. We definitely want to show HTTP message details (url, header, verb) somewhere, but do we want to let the user edit the request using some special controls? Like, set URL or headers, cookies manually. Not in the form, but on a separate tab.

Imagine something like this, but editable

![[Notion 2/Attachments/Untitled 1 3.png|Untitled 1 3.png]]

I guess, we don’t need this for now, but I want clear that out.

**So, in a nutshell: just the form or the form + special controls for HTTP?**

Do we need an ability to send arbitrary HTTP requests in our plugin or just those defined in OpenAPI spec? I guess, no need in arbitrary requests, since we stated it’s a **REST** plugin, not HTTP in general.

  

Или вся эта protocol-specific информация должна на отдельной вкладке отображаться? Так, наверно, лучше будет. Есть форма, а есть более fine-grained доступ. Если нужно. Если не нужно — оставить read-only. Будет удобнее создавать из ISession: два отдельных метода.

Придётся как-то переделывать обратно, возвращать формы.ddsdsdsdsds
---
Created: 2021-09-30T19:34
Updated: 2022-04-11T19:41
---
Приготовления
Новый класс Message: general, headers, body
Стоит ли менять реализацию на Jackson?
Разделение на Response и Request
Плагины
REST plugin
Connected
Какой HTTP клиент использовать?
Schema
Обойтись без схемы сначала?
Аутентификация
Другие продукты
SOAP UI
Задачи
Open API
Custom New Session view
OpenAPI Session
Привести в порядок методы, создающие IMessage и protocolMessage
Текущие задачи/вопросы
# Приготовления
В Message должны быть поля headers, body, general. General — в зависимости от протокола. Например, для REST/WS там нужно показывать URL, status code (это только во Viewer?). Для других протоколов — иные свойства. Следовательно, нужно ещё и где-то связать UI control с секцией General. Как получать данные из контрола?
Нужно ли в Builder показывать status code? Нет, status code отправляет сервер с Response. Пока мы его не будем валидировать, чтобы было проще.
Нужно разделить сущности Message и то-что-показываем-в-таблице (IScenarioStep?). Почему?
- Во-первых, у steps в Builder и во Viewer разные свойства/поля, но сейчас они определены в IScenarioStep/Message для них обоих.
    - executionState. При отправке, во Viewer не используется. Но теоретически можно. Но пока не нужно. States другие, нежели для Builder, где это свойство используется
    - IScenarioStep\#toExplainString — это в builder и для установки description во время копирования. Должен остаться в IScenarioStep
    - skip — только Builder
    - breakpoint — только Builder
    - description — только Builder
    - getForm — для Viewer не нужный метод. При создание ScenarioStepBase форма присваивается в поле, а она не всегда нужна
    - getTimestamp — только для Viewer
- Во-вторых, где определим `IScenarioStep\#getFirstLine`, `IScenarioStep\#getSecondLine, toExplainString` ==Нужен ли специальный форматтер для этого?==
По видимому, IScenarioStep должен содержать Message. Сам IScenarioStep и будет содержать все нужные свойства, специфичные для Builder. Ещё один вопрос — для форматирования превьюхи сообщения (json, text) создаётся protocol message. Не очень красиво.
Если это действительно необходимо, можно использовать один класс таблицы и в Builder, и в Viewer, и если нет другого способа адаптировать эту таблицу под разные типы сущностей (например, с помощью valueFactory), использовать паттерн Adapter. Т.е. необязательно тащить какой-то интерфейс, содержащий информацию о UI, и реализовывать его в классах Message и ScenarioStep, только чтобы показать сообщение в таблице.
Ну и конечно, первое, с чего стоит начать — создать интерфейс ProtocolMessageFormatter. И, видимо, убрать `asRawString, asPrettyString, asTreeString`. Написать тесты к нему.
Все эти изменения затронут persistence.
Нужно ли срочно растаскивать Builder и Viewer? Новый View или класс TableView можно назвать FlowTable. Начать можно с того, чтобы определить, какие контролы будут во Viewer, а какие — в Builder, какая функциональность (copy-paste, ещё что-то). Если хотим отделить полученные, _настоящие,_ сообщения от шагов в Builder, то это однозначно стоит сделать.
Поскольку раньше использовался таймер как один из IScenarioStep, имеет смысл оставить IScenarioStep интерфейсом и реализовать как MessageScenarioStep. Метод `execute` должен остаться только в IScenarioStep. В реализации MessageScenarioStep `execute` должен обращаться к ISession напрямую и отправлять с её помощью сообщение, не нужно обращаться к форме.
## Новый класс Message: general, headers, body
Нужно дать ясные определения этому всему, а конце концов определить для каждого протокола, что есть что. На данный момент Headers и General не будут валидироваться.
**Headers** — мапа с произвольным порядком`<String, String>`. Доставать оттуда данные нужно будет для показа в UI, требований к локализации нет пока, поэтому тип такой. Записывать будем при создании, в реализации ISession.
**General** зависит от протокола. Та же `Map<String, String>`, только (скорее всего) будем по-разному показывать данные из неё в UI. Те самые HTTP method, status и т.д.
**Body**. Дерево, которое рендерится формой. Пока в json-формате. Или header/footer тоже должны рендериться формой?
Нужен ли footer/trailer? В FIX есть такое понятие. Можно его сделать опциональным. Опциональны и headers, и body. Добавить `hasHeader()` методы?
==Нужен ли== ==**protocolMessage**== ==и его форматтер? Не должен ли форматтер работать с body? Есть ли смысл вообще хранить protocolMessage?==
Для чего сейчас он используется? Для того, чтобы форматировать сообщение. Что если сразу преобразовывать protocolMessage в некий JSON, а затем его форматировать для показа пользователю? Вроде нет, но сейчас наши форматтеры написаны под protocolMessage → JSON.
Что будут форматировать форматтеры? Что будут принимать: Message или protocol message? Будут принимать Message. Но, возможно, придётся отказаться от форматтеров и давать из плагина вид полностью.
Методы `se.suncom.multiq.interfaces.ISession\#createMessage` и `se.suncom.multiq.interfaces.ISession\#createProtocolMessage`. Выглядят довольно грязно.
Сообщение для отправки из JSON десереализует ISession.
Если Message будет создаваться всегда внутри сессии (а так и должно быть, если мы разделим ScenarioStep и Message), то интерфейс IMessage не нужен, нужен конкретный класс.
Проблема: для HTTP запросы с глаголами GET/DELETE и др. не могут иметь тело. Но могут иметь Headers. Нет, не проблема. Будет пустое body, т.е. null.
Или всё-таки иметь immutable final Message и какое-нибудь поле CustomData, которое будет TypeParameter в Session. Есть ли смысл? Не хочется иметь Headers untyped.
В FIX в Header, который является FieldMap, могут входить и Groups, т.е. Header в этом случае может иметь несколько уровней вложения теоретически. А как на самом деле?
Заодно нужно избавиться, если возможно, от типа Actor. В Message он не нужен, не нужны там методы from и to. Есть isOutbound, isInbound. Ни outbound, ни inbound может быть только IScenarioStep.
В форматтеры будет тогда передаваться Message, в них будем работать с message body, которое в формате JSON. Нет информации о полях, это неудобно. Хотя, если за счёт этого получится избавиться от protocolMessage:<Object> везде, то хорошо, наверно. Но информация о том, как работать с JSON-представлением (какие поля что значат), будет разбросана в разных местах.
А ещё для se.suncom.multiq.plugin.fix.FixMessageFormatter\#toRawString существующее сообщение обновялется данными из сесии, когда она становится подключенной, в противном случае мы показываем ошибку “Session is not connected”.
Что если не убирать protocolMessage (полезно для форматтеров), а формировать header и trailer на его основе.
Интересно, что разделение на Trailer, Footer, Body нам пригодится только для создания формы. Не лушче ли создавать формы с разными секциями прямо из protocolMessage?
### Стоит ли менять реализацию на Jackson?
# Разделение на Response и Request
Подтипы Message? Подсмотреть в RestEasy и других http клиентах.
==Нужно ли это разделение? Для каких протоколов оно имеет смысл, для каких — нет?==
Скажем, в теле http-запроса мы можем отправить одну сущность, а в ответе получить другую. Это ок.
**FIX** Some FIX messages like ExecutionReport message are responses already.
**SSH**. Всё внутри.
# Плагины
Прежде, чем начать работу, нужно удалить/закомментировать WS-плагины, потому что они сильно сломаны, будут мешать рефакторингу.
Проблемы с нынешним WS-плагином:
- Во-первых, там всякие неочевидные инициализации через вызов геттеров. В этих же геттерах происходит обращение к файловой системе. В общем, всё очень плохо. Ну, это и так ясно.
- В диалоге создания WS-сессии wadl-path — просто строка. Относительно чего этот путь? К какому файлу он должен вести? Обязателен ли он. Лучше file chooser и какое-то описание в tooltip.
- Не нужно сразу подключаться к сессии. Слишком долгий таймаут. Предоставить возможность добавить сессию без подключения. Либо добавить кнопку, чтобы отменить подключение.
Стоит заранее отделить плагины в отдельные проекты и добавить к ним в зависимости зависимость от некоего проекта с API. Сейчас не много зависимостей от ядра проекта.
## REST plugin
==Нужен ли ему какой-то кастомный UI?==
==Как указывать параметры URL?==
Создавать вид под каждую секцию из Message. HTTP-метод точно надо выбирать из списка.
Содержимое запроса (body) может иметь разную форму: application/x-www-form-urlencoded, application/json, да хоть plain text. А у нас всё строится на парадигме, что у каждого ScenarioStep есть форма. Это проблема. Если у нас REST, то с ним обычно используется JSON, но это отнюдь не обязательно. Может быть и XML, и yaml. Но форма — это только для отправки. Мы можем визуализировать уже полученное сообщение как угодно, и не важно, что мы интерфейс отправки в виде формы.
Вообще в ответ может прийти что угодно. И файл тоже. Его пользователь может захотеть валидировать по размеру файла или по чек-сумме. Строя сценарий в Builder, мы определяем и ожидаемый Response. Но когда мы получаем во Viewer, там уже надо как-то определять, как его визуализировать. Возможно, предложить пользователю выбрать.
Сейчас у нас три представления для полученных сообщений: raw, pretty, tree (в UI называются Plain, Tree, Raw). В Raw можно показывать текстовый контент без форматирования. В pretty — форматированный. Опять же, там должен быть выбор форматтера. Значит, вид нужно создавать в плагине. Какой смысл в Tree view? Он позволяет удобно искать по полям, подсвечивает совпадения.
Новый вид нужно создавать в плагине или в сессии на основе Message. Хотя, это даже не обязательно. Если не будет автоматического определения (JSON/XML/etc). Вид просто можно создавать в плагине. А автоматическое определение будет делать сам компонент, когда в него будет устанавливаться Message.
Новый вид назовём Pretty или как-то похоже, он заменит нынешний Plain. Потому что сейчас Plain и Raw во многом похожи: для SSH они одинаковы, а для FIX содержимое просто немного по-разному отформатировано. ==В связи с этим, нужно пересмотреть задачу, где нужно создать интерфейс форматтера.==
Надо подойти к этому с точки зрения UI/UX. Сначала набросать кнопочки. Как будет удобно пользователю? Потом думать о структуре.
Куки можно пока показывать как обычные хедеры, но потом было бы удобнее иметь для них отдельную секцию.
Какие Responses захочет валидировать пользователь:
==Нужно почитать про структуру HTTP запроса.==
### Connected
REST плагин не может быть connected или disconnected, это бессмысленно. В существующих WS-плагинах по вызову `connect` парсится конфиг, плюс в RWS-делается какой-то пустой запрос для проверки, что сервер достижим.
### Какой HTTP клиент использовать?
**Java 9**. Может быть синхронным и асинхронным.
Если можно использовать внутренние классы RestEasy — хорошо. [Здесь](https://github.com/resteasy/resteasy-examples/tree/main/wadl-example/) есть пример использования RestEasy для WADL.
Требования:
- Поддержка HTTP 2.0?
### Schema
Swagger (Open API). Правой кнопкой кликаем на сессии → выбираем тип сообщения. У нас сейчас всё завязано на типах, на схеме. Просто какой-нибудь JSON (или не JSON) мы отправить не можем. Схема содержит content type.
Какие минимальные изменения можно сделать, чтобы мы могли отправлять произвольные запросы?
- Редактор, который валидирует синтакс
- Определить форму более общо. Как некий контрол, который создаёт model. А кто тогда отправлять будет model?
Если будем реализовывать схему, нужно будет конвертировать OpenAPI definition в JSON schema, потом передавать это в SchemaForm. Разве сейчас я так не делаю уже где-то? Это повторяющееся действие. `se.suncom.multiq.plugin.fix.FixSession\#getJsonSchema` вызывается только из SchemaForm при том, что ShemaForm создаётся тоже в ISession. jsonSchema нужно определять при создании SchemaForm, устанавливать полем.
### Обойтись без схемы сначала?
==Нужно ли нам прямо сейчас заморачиваться со схемой?== Может, начать с текстового контента? Пользователь сможет выбирать, как показывать респонс. Или он будет выбираться на основе content type. А как валидировать? Ясно, что лучше выделить валидацию из ValidationForm в отдельный класс вроде Validator. Отделить вид от логики. А что это значит фактически? Что будет общее между разными View для отправки? И какими они будут?
Если начнём с простого (просто валидируем тело запроса), то можно просто сравнивать текстовое содержимое, и показывать дифф (в отдельном диалоговом окне, например). Пригодятся настройки:
- учитывать ли переносы строк и пробелы при валидации
- нужно будет выделять неправильный синтаксис. Посмотреть [highlight.fx](https://github.com/eugener/highlight.fx) и [RichTextFX](https://github.com/FXMisc/RichTextFX). [highlight.fx](https://github.com/eugener/highlight.fx): нет лексера для JSON и подобных форматов. Эти вьюхи (но без проверки синтаксиса) будут полезны и так.
## Аутентификация
![[Untitled 13.png|Untitled 13.png]]
Можно вьюху скопировать. Для
# Другие продукты
Нужно посмотреть, как другие инструменты сделаны. На что смотреть?
## SOAP UI
[https://www.soapui.org/tools/readyapi/](https://www.soapui.org/tools/readyapi/)
[https://www.soapui.org/tools/soapui/](https://www.soapui.org/tools/soapui/)

> [!info] SOAP Web Service Example | Getting Started with API Testing | SoapUI  
> While SoapUI Open Source can be seen as the Swiss Army knife for testing, ReadyAPI is the tool with the sharpest edge.  
> [https://www.soapui.org/resources/tutorials/soap-sample-project/](https://www.soapui.org/resources/tutorials/soap-sample-project/)  
# Задачи
Учесть, что придётся и тесты писать на некоторые компоненты. И чинить старые.
- [ ] Move plugins to separate Gradle projects
    
    This is essential for us to be able to ship different builds for customers. Separating plugin implementation from the application itself early allows us to avoid issues with tight coupling later. The sooner, the better.
    
- [ ] Implement MessageFormatter interface (conform `FixMessageUtil`, `ItchMessageUtil` to the same structure).
    
    We have a few classes (`FixMessageUtil`, `ItchMessageUtil`) that do a very similar job, but they are poorly structured and thus hard to maintain. As they do the same job, they should implement a common interface).
    
    ```Java
    public interface IMessageFormatter {
        String toRawString(Message message);
    
        String toTreeString(Message message);
    
        String toPrettyString(Message message);
    }
    ```
    
    Once the interface is introduced we will be able to remove `**asRawString**`**,**`**asPrettyString**`**,** `**asTreeString**` observable properties from Message classes. Observable properties should be kept closer to UI (just where they are needed) to reduce memory consumption and make debugging easier. Then the message formatter instance should be used in `FormTabsPresenter` instead of these properties.
    
    Write tests for it.
    
- [ ] Separate `Message` from `IScenarioStep`
    
    `IMessage` extends `IScenarioStep` at the moment and therefore inherits properties specific to a step in a Test Scenario only such as `isBreakPoint`, `description`, `skipProperty` and others that make sense only in a context of a Test Scenario. But a Message can exist without a TestScenario. To make our design cleaner and to reduce memory consumption, we should separate `Message` from `IScenarioStep`. We should introduce `MessageScenarioStep` implementation of `IScenarioStep` that would include (or create) a `Message` instance.
    
- [ ] Introduce _general_, _header,_ _body, trailer/footer_ sections to Message
    
    Header, trailer and general sections are Maps<String, String> with custom order (defined by the plugin). Body is a JSON object. Body is the message payload in case of HTTP, the message body. Should give a closer look to other plugins as to what's going to be in footer or body, etc. Ideally, body should contain just the information needed for the form. No more, no less. Body, header and trailer can be empty.
    
    _General_ information is about the message that is not the part of the message fields itself (URL, HTTP method, HTTP status code, etc). _Trailer_ and _footer_ are protocol-specific.
    
    Plugin should be able to provide a custom view/control for General section itself or for its sections independetly, whatever works best.
    
    Existing plugins must be changed to adapt the new Message structure.
    
    - [ ] Adapt existing plugins. Separate messages into sections.
    - [ ] Modify UI
    - [ ] We should change ValidationForm to make it possible to validate header, general and footer sections. Perhaps, in the same fashion as now, only there will be a separate validation table for each message section.
    - [ ] Do not store original protocol message anywhere, use its JSON representation.
        
        The original protocol message is used for the purpose of formatting preview in Plain, Raw, Tree tabs. Its created whenever a Form changes. Plugin or Session should convert the original protocol message into a Message upon reception. Plugin or Session should be able to restore a Message back into the original protocol message. Tests may be very handful here.
        
- [ ] Let plugins provide a custom view for a message among Raw and Tree tabs.
    
    The user should be able to view a message based on its content type header in case of a HTTP message. The plugin should provide a predefined view that would work best for this particular message/plugin (let's call it CustomMessageView) instead of existing Plain view (Plain tab). Say, if the content type of the message is `application/json`, message body should be formatted as JSON text with syntax highlighting. It will be also very useful to make the nodes of a JSON object expandable in a TreeView fashion (just like in Tree tab currently). The HTTP plugin will be able to provide a ChoiceBox to select the message formatter (JSON/XML or other) manually.
    
    It's up to CustomMessageView to decide how to render a specific Message, no need to pass this decision to Plugin directly.
    
    TODO: How to structure the UI, message sections (header, footer, body) and message views (CustomMessageView, Raw, Tree). Should Tree include header of an HTTP message in the future? Is it possible to make a CustomMessageView that will eliminate a need in Tree view?
    
- [ ] Separate Messages into Requests and Responses.
    
    Some **FIX** messages like ExecutionReport message are responses already.
    
    **ITCH** messages can be inbound only, right?
    
- [ ] Implement HTTP protocol
    
    - [ ] Choose client implementation
        - [ ] Use latest Java?
    - [ ] Add API key and Basic authentication to New session dialog.
        
        For API key add a ChoiceBox to select where to put the key.
        
        ![[Untitled 13.png|Untitled 13.png]]
        
        Postman API key authentication screen
        
        The view should be provided by the plugin.
        
    - [ ] Start with plain HTTP without schema support.
        
        Provide a text editor for http requests instead of SchemaForm. We can't validate a text response now, because it does not conform to a certain schema. That's why we'll skip validation for this step. But if you're interested in ability to validate an arbitrary text response, we can implement that.
        
    - [ ] Implement Open API schema import
        - [ ] Change New session dialog
        - [ ] Implement parsing. Use [OpenAPI generator](https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator-core/src/main/java/org/openapitools/codegen/api) classes?
        - [ ] Generate UI schema for the SchemaForm
        - [ ] Implement the dialog for form selection in Session pane (When creating a new form in Workspace).
    
      
    
# Open API
Задачи:
- Создать messageTypes/actions — из Operations. Из messageTypes можно возвращать не List<String>, а List<IMessageSpecification>. Реализация IMessageSpecification — в плагине своя, если нужно. Обдумать.
- Конвертировать Operation в Schema и Ui Schema
    - Параметры запроса (cookie, path, headers)
    - Тело запроса. Отдельный пункт body в форме
- Нужно ли сохранять swagger.yml? Или всё будет записано в сообщениях?
  
- Преобразовать объект Operation в json schema
- Извлечь из form model **параметры**
- Извлечь из form model **тело.** Тело может быть файлом/а не string entity. Но возвращать можно и InputStream. Что для StringEntity, что для FileEntity.
## Custom New Session view
Что показать на экране создания OpenAPI сессии?
- Способ аутентификации (отдельная владка, как в Postman?):
    
    ![[Untitled 1 6.png|Untitled 1 6.png]]
    
    - No authentication
    - Basic
    - Basic session settings
        
        - Color
        - Icon (badge)
        - Gateway
            
            Возможно, в будущем — ComboBox для выбора из определенных в спецификации
            
        - Port
        
        Здесь же секция для получения OpenAPI из удаленного источника?
        
    
    Может, и создавать Session в этом view, а не где-то ещё? Абстрактный метод, который возвращает Session.
    
# OpenAPI Session
HttpResponse нужно показывать как стрелку от сервера.
Как сохранять произвольный ответ сервера. Как будем сохранять стандартные запросы? Нам не нужно сохранять произвольный ответ сервера. Только форму для ValidationForm! Вернее, ожидаемый респонс.
## Привести в порядок методы, создающие IMessage и protocolMessage
В каких случаях нужно создавать сообщения:
- Получили от сервера
    
    `se.suncom.multiq.interfaces.impl.SessionBase\#createMessage`
    
- Создали новый `IScenarioStep`, когда редактировали сценарий. Передали пустой JSON.
    
    `se.suncom.multiq.interfaces.ISession\#createOutboundMessage`
    
    `se.suncom.multiq.interfaces.ISession\#createInboundMessage`
    
- Загрузили новый сценарий с диска
    
    `se.suncom.multiq.interfaces.ISession\#createOutboundMessage`
    
    `se.suncom.multiq.interfaces.ISession\#createInboundMessage`
    
- Сериализация выбранных сообщений
    
    `se.suncom.multiq.interfaces.ISession\#createOutboundMessage`
    
    `se.suncom.multiq.interfaces.ISession\#createInboundMessage`
    
## Текущие задачи/вопросы
- [x] В каком формате представляются Inbound messages, когда сохраняется сценарий?
    
    В таком же, в каком и outbound форма. Для FIX, к примеру.
    
- [ ] Как прочитать response entity и при этом сохранить данные о респонсе: статус код, заголовки? Какой класс использовать?
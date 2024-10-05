Вызывать After Effects, запуская скрипт, нужно так:

```Plain
"c:\Program Files\Adobe\Adobe After Effects CC 2018\Support Files\AfterFX.com" -r "c:\projects\upwork\edu martinez\testing\main.jsxbin"
```

Относительные пути будут нормально работать, если запускать jsx-файл, но если запускать их из ESTK, рабочая директория будет в ProgramFiles и возможны ошибки.

Если запускаем скрипт из командной строки, и там пишем в $.writeln(), то если ESTK открыт, он получит эти сообщения.

**AE + AME**

AE 2018 крашится, если передаём композицию на рендер в AME скриптом и закрываем проект (без сохранения изменений).

из AE 2019 можно передавать несколько компах на рендеринг и даже закрывать проекты в промежутке, все компахи будут переданы в AME, но приложение виснeт и через некоторое время появляется окно крэша.

Если в скрипте прописать app.quit(), то AME не успевает запуститься и получить команду. А если запускать скрипт с работающим AME, то AE крашится.

Если AME запущен, и пытаемся отрендерить несколько проектов в одном открытом инстансе AE, AE падает.

Получилось запустить AE, открыть проект той же версии, что и открытый AE, и передать данные в открытый AME, но AE всё равно крашится.

```Plain
app.beginSuppressDialogs()




function render() {
    var projectFile = new File('c:\\temp\\ame-wf-test (converted).aep')




    app.open(projectFile)




    var rqItem = app.project.renderQueue.items.add(app.project.item(1))
    rqItem.logType = LogType.ERRORS_AND_PER_FRAME_INFO
    var aviOutputFile = new File('c:\\temp\\test-out\\output.avi')
    rqItem.outputModules[1].file = aviOutputFile




    app.project.renderQueue.queueInAME(false)
    app.project.close(CloseOptions.DO_NOT_SAVE_CHANGES)
}




for (var i = 0; i <1; i++)
{
    render()
}


app.quit()
```

Так что выход — сохранять отдельный проект в Watch Folder AME и оставлять только одну композицию в самом верхнем уровне, AME отрендерит только её.

aequery - либа что надо

**CEP**

В этом стартере [https://github.com/fusepilot/parcel-plugin-cep-starter](https://github.com/fusepilot/parcel-plugin-cep-starter) команда create-zxp криво работает, потому что пути, содержащие пробелы, передаются без кавычек.

Ещё запуск yarn'ом не работает, приходится сначала устанавливать: npm install

Можно посмотреть свежие версии либ.

Не забыть про манифест! Он не генерируется в сборке.

Попробовать другую сборку.

А вообще, можно сделать на чистом html? Но хорошо бы проверить, что у пользователя включен доступ скриптов к интернету

**Reflection**

Get properties

```Plain
var f = new File ("myfile");
var props = f.reflect.properties;
for (var i = 0; i < props.length; i++) {
    $.writeln(’this property ’ + props[i].name + ’ is ’ + f[props[i].name]);
}
```
---
Created: 2023-11-17T17:40
"Issue #": 152
tags:
  - JavaFX-Bug
Updated: 2023-11-17T17:44
---
Если установить `setContextMenuEnabled`=false в FXML, он не применяется в WebView.
  
```JavaScript
webView.getEngine().load(StorageUtil.getJsonViewerUri().toString());
webView.setContextMenuEnabled(false);
```
А если в конроллере, то применяется. Причём, не важно, после загрузки страницы вызвали или перед.
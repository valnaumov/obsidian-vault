---
Created: 2023-10-23T22:21
Updated: 2023-11-07T22:05
---
- [ ] If no response is defined for a particular endpoint + statusCode, NPE is thrown. Need some kind of a default response. Probably, it also should not be possible to add this default response in Builder, and should not be possible to copy from Viewer either. Probably, yes. Or a default type of response for every status code that is going to be used if no response is defined for a given endpoint + statusCode.
- [x] basePath field from Open API (Swagger, at least) is not used in IntelliQ. It should be the default base path for every request. But it should be also possible to add yet another prefix to this basePath, we have a text field for that in New Session dialog.
- [ ] setting API key authentication in NewSessionDialog does not seem to have effect. Header is not added for requests. Edit: it’s probably set later in send method. The original message passed to send does not contain all the headers to be sent.
- [ ] Show full path (scheme, protocol, host) in MessageFormatter of OpenAPI Session
- [ ] In environments window, host availability detection does not work for
    
    - [ ] [petstore.swagger.io](http://petstore.swagger.io/)
    - [ ] [api-test.riksbank.se](http://api-test.riksbank.se/)
    
    Probably, they both don’t respond to ping requests and do not allow HTTP in favour of HTTPS
    

  

- [ ] \#58 should indicate progress: message is sent, waiting for response? Leave some feedback for Tobbe
- [ ] Set FIX version property

  

\#200

- [x] Determine version
- [x] Rename Session class
- [x] Correct basePath?
- [x] Commit the demo project
- [x] Option: https or not
- [x] Make sure Riksbank public API works
- [ ] Write host header into formatted message. Also, need to identify somehow an http request
    - [ ] Host
        
        The original `ClassicHttpRequest` is copied before execution. From wire logging we can tell the headers:
        
        "Accept-Encoding: gzip, x-gzip, deflate"  
        "Host: 162.55.175.66:9966"  
        "Connection: keep-alive"  
        "User-Agent: MultiQ 1.0.0-SNAPSHOT"  
        
        Use `HttpRequestInterceptor`? But then we need to make IMessage mutable. And toPlainString and toRawString then need to be made Vals
        
          
        
- [ ] In NewSession dialog, move everything to the same screen.
- [x] Allow yaml files
- [x] the "required" flag does not work for Riksbanken API (it works for Petstore)
    
    Is not set for path parameters.
    
- [ ] Handle unexpected (undefined in the spec) responses. It should be safe for responses, since we don’t have to create forms. Expected response is just a tree structure (JSON). But we should not be able to selected and add these responses from Builder. Or should we?
    
    Copying is ok.
    
- [ ] Add sessions to demo project:
    - [ ] Make sure ours works and the correct spec is used
    - [ ] [https://petstore3.swagger.io](https://petstore3.swagger.io/)
    - [ ] petstore swagger 2
    - [ ] Riksbank public API
- [x] basePath
    - [x] not detected correctly for OpenAPI 3 (`/v3` instead of `/api/v3`)
        
        For OpenAPI 3 server.getUrl returns `/api/v3`Then the path is extracted (should not be).
        
        In case of Swagger 2.0 server.getUrl returns `[https://petstore.swagger.io/v2](https://petstore.swagger.io/v2)` .
        
        Need to tell the difference
        
    - [ ] Besides, [Server Templating](https://swagger.io/docs/specification/api-host-and-base-path/#templating) (for url) can be used. Ignore that?
- [x] Use "summary" field instead of "operationId" to show the message names
    
    Implement using first line?
    
- [ ] Check that the parameter value is set to the data model initially for dropdowns. Could be broken by Elias. Check before and after his commit
    
    Probably, I
    
- [ ] Optional: drag’n’drop for Select File button
- [x] Add more session properties for OpenAPI session
    - [x] Use HTTPS
    - [x] Base URL
    - [ ] Authentication-related

> [!info]  
>  
> [https://github.com/OAI/OpenAPI-Specification/tree/main/examples](https://github.com/OAI/OpenAPI-Specification/tree/main/examples)  

Some spec examples
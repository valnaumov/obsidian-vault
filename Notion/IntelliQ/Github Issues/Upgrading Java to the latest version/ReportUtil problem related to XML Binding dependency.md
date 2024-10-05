TODO paste exception here

> [!info]  
>  
> [https://bugs.openjdk.org/browse/JDK-8170042](https://bugs.openjdk.org/browse/JDK-8170042)  
JDK 9 issue
Two ways to solve (to try solving):
- Add opens for java.lang (or what was it) module/package
- Replace the XML Binding API library (`_jakarta.xml.bind-api_`) and XML Binding Implementation library.
    - TODO: is it possible to keep API intact, but change the implementation for a library that does not call
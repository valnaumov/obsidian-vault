- [ ] Introduce a dummy class MessageSpecification with just one field: String messageType.
    
    ```Java
    class MessageSpecification {
    	String messageType
    }
    ```
    
    Replace messageType usages. Use MessageSpecification class instance where possible. Where it is not possible and a string is needed, refer to its messageType field (via getter, of course).
    
    MessageSpecifications should be stored in the Session class and be reused (so as not to create multiple instances for the same message type and break the logic somewhere). Will it be possible?
    
    - [x] `OpenAPISession\#messageSpecificationByMessageType` should have first type of `MessageType`
    - [x] SearchAndReplace panel
    - [ ] Rename fields in MessageDTO and other DTOs to be messageTypeId rather than just messageType?
    - [x] `MessageReceiver`
    - [ ] Check that MessageType instance equallity works. We may want to check MessageType instances equality by messageType (messageId) field for now.
- [ ] MessageSpecification / MessageType class should be constructed in ISession and, if needed, retrieved from the ISession via some `lookupMessageSpecification(String messageType)` method
- [ ] Introduce inbound/outbound enum?
- [ ] Store additional data in MessageSpecification like description?
What `getOutboundSessionMenu` currently does:
- Returns all outbound message types.
- Groups outbound message types. Groups can be nested and contain message types as well as other groups.
- Add forms on the Desktop (using MenuItem’s onAction handler).
- Reads formDef files to override form titles. Looks them up by messageType.json. This is also done in `SessionBase\#getFormDefinition`. Code duplication
- Associate icons and graphics with messageTypes. We don’t have to use MessageType class to provide these though. A separate UISomethingFactory can be used.
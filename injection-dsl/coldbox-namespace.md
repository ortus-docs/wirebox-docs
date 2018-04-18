# ColdBox Namespace

This namespace is a combination of namespaces that are only active when used within a ColdBox application:

| DSL | Description |
| --- | --- |
| coldbox | Get the coldbox controller reference ||
| coldbox:configSettings | Get a reference to the application's configuration settings |
| coldbox:dataMarshaller | Get a reference to the application's data marshaller |
| coldbox:flash | Get a reference to the application's flash scope object |
| coldbox:fwSetting | Get a reference to the framework settings |
| coldbox:fwSetting:{setting} | Get a setting from the ColdBox settings instead of the Application settings |
| coldbox:handlerService | Get a reference to the handler service |
| coldbox:interceptorService | Get a reference to the interceptor service |
| coldbox:loaderService | Get a reference to the loader service |


| coldbox:setting:{setting} | Get the coldbox application _{setting}_ setting and inject it |
| coldbox:setting:{setting}@{module} | Get the coldbox application _{setting}_ from the _{module}_ and inject it |
| coldbox:datasource:{alias} | Get a new datasource bean according to _{alias}_ |
| coldbox:configBean | Get a new config bean object and inject it |
| coldbox:mailsettingsbean | Get a new mail settings bean and inject it |
| coldbox:requestContext | Get a reference to the current transient request context |
| coldbox:requestService | Get a reference to the request service |
| coldbox:debuggerService | Get a reference to the debugger service |
| coldbox:routingService | Get a reference to the routing service |
| coldbox:moduleService | Get a reference to the ColdBox Module Service |
| coldbox:interceptor:{name} | Get a reference of a named interceptor _{name}_ |
| coldbox:cacheManager | get the cache manager |
| coldbox:fwConfigBean | Get a configuration bean object with ColdBox settings instead of Application settings |
| coldbox:moduleSettings:{module} | Inject the entire _{module}_ settings structure |
| coldbox:moduleConfig:{module} | Inject the entire _{module}_ configurations structure |


```javascript
// some examples
property name="logbox" inject="logbox";
property name="rootLogger" inject="logbox:root";
property name="logger" inject="logbox:logger:model.com.UserService";
property name="moduleService" inject="coldbox:moduleService";
property name="producer" inject="coldbox:interceptor:MessageProducer";
property name="configBean" inject="coldbox:fwConfigBean";
property name="producer" inject="interceptor:MessageProducer";
property name="appPath" inject="coldbox:fwSetting:ApplicationPath";

// JavaLoader goodness
property name="binaryHeap" inject="javaLoader:org.apache.commons.collections.BinaryHeap";
property name="email" inject="javaLoader:org.apache.commons.mail.SimpleEmail";
```


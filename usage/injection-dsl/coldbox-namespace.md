# ColdBox Namespace

This namespace is a combination of namespaces that are only active when used within a ColdBox application:

## Single Stage Injections

| DSL     | Description                          |   |
| ------- | ------------------------------------ | - |
| coldbox | Get the coldbox controller reference |   |

## Two Stage Injections

| DSL                        | Description                                                 |
| -------------------------- | ----------------------------------------------------------- |
| coldbox:configSettings     | Get a reference to the application's configuration settings |
| coldbox:dataMarshaller     | Get a reference to the application's data marshaller        |
| coldbox:flash              | Get a reference to the application's flash scope object     |
| coldbox:fwSetting          | Get a reference to the framework settings                   |
| coldbox:handlerService     | Get a reference to the handler service                      |
| coldbox:interceptorService | Get a reference to the interceptor service                  |
| coldbox:loaderService      | Get a reference to the loader service                       |
| coldbox:moduleService      | Get a reference to the ColdBox Module Service               |
| coldbox:requestContext     | Get a reference to the current transient request context    |
| coldbox:requestService     | Get a reference to the request service                      |
| coldbox:router             | Get a reference to the application router object            |
| coldbox:routingService     | Get a reference to the routing service                      |
| coldbox:renderer           | Get a reference to a ColdBox renderer object                |

## Three Stage Injections

| DSL                                | Description                                                                 |
| ---------------------------------- | --------------------------------------------------------------------------- |
| coldbox:fwSetting:{setting}        | Get a setting from the ColdBox settings instead of the Application settings |
| coldbox:setting:{setting}          | Get the coldbox application _{setting}_ setting and inject it               |
| coldbox:setting:{setting}@{module} | Get the coldbox application _{setting}_ from the _{module}_ and inject it   |
| coldbox:interceptor:{name}         | Get a reference of a named interceptor _{name}_                             |
| coldbox:moduleSettings:{module}    | Inject the entire _{module}_ settings structure                             |
| coldbox:moduleConfig:{module}      | Inject the entire _{module}_ configurations structure                       |

## Examples

```javascript
// some examples
property name="logbox" inject="logbox";
property name="rootLogger" inject="logbox:root";
property name="logger" inject="logbox:logger:model.com.UserService";
property name="moduleService" inject="coldbox:moduleService";
property name="producer" inject="coldbox:interceptor:MessageProducer";
property name="producer" inject="interceptor:MessageProducer";
property name="appPath" inject="coldbox:fwSetting:ApplicationPath";
```

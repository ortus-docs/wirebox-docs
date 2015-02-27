# Property Annotation

Every `cfproperty` can be annotated with our injection annotations:

* `@inject` : The injection DSL
* `@scope` : The visibility scope to inject the dependency into. By default it injects into variables scope

```javascript
property name="service" inject="id:MyService";

property name="TYPES" inject="id:CustomTypes" scope="this";

property name="roles" inject="id:RoleService:getRoles" scope="instance";
```

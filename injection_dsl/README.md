# Injection DSL

The injection DSL is a domain specific language that denotes what to inject in the current placeholder: property, argument, or method via the inject annotation. This injection DSL not only can it be used via annotations but also via our mapping DSL whenever a `dsl` argument can be used. This DSL is constructed by joining words separated by a `:` colon. The first part of this string is what we will denote as the injection **DSL Namespace**.

```javascript
inject="{namespace}:extra:extra:extra"
```

## Property Annotation

Every `cfproperty` can be annotated with our injection annotations:

* `@inject` : The injection DSL
* `@scope` : The visibility scope to inject the dependency into. By default it injects into `variables` scope

```javascript
property name="service" inject="id:MyService";

property name="TYPES" inject="id:CustomTypes" scope="this";

property name="roles" inject="id:RoleService:getRoles" scope="instance";
```

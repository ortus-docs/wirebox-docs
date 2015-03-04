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

## Constructor Argument Annotation

You can also annotated constructor arguments with the inject annotation.

```javascript
<---  Via tag based annotations --->
<cffunction name="init" returntype="any" output="false">
	<cfargument name="myService" inject="UserService">
	<cfargument name="cache" 	 inject="cachebox:default">

</cffunction>


// Via script but alternative method as inline annotations are broken in ACF

/**
* Init
* @myService.inject UserService
* @cache.inject cachebox:default
*/
function init(required myService, required cache){
}
```

> **Caution** In full script components, annotating inline arguments is broken in Adobe ColdFusion 9. You will have to annotate them via the alternative annotation syntax in ColdFusion 9 via the javadocs style comments.


## Setter Method Annotation

You can also annotate setter methods with the inject annotation to provide injections

```javascript
<---  Via tag based annotations --->
<cffunction name="setService" returntype="any" output="false" inject="UserService">
	<cfargument name="service">
</cffunction>


function setService(required service) inject="UserService"{
  variables.service = arguments.service;
}
```

WireBox offers a wide gamut of annotation namespaces you can use in your CFML applications and ColdBox applications. However, we took it a step further and allowed you to create your own custom DSL namespaces making your annotations come alive!

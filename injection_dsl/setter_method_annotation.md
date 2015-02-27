# Setter Method Annotation

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

WireBox offers a wide gamut of annotation namespaces you can use in your CFML applications and ColdBox applications. However, we took it a step further and allowed you to create your own custom DSL namespaces making your annotations come alive! So let's investigate the shipped namespaces:

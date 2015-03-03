# Constructor Argument Annotation

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

> **Important** In full script components, annotating inline arguments is broken in Adobe ColdFusion 9. You will have to annotate them via the alternative annotation syntax in ColdFusion 9 via the javadocs style comments.

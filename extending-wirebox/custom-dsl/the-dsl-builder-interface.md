# The DSL Builder Interface

```javascript
customDSL = {
    ortus = "path.model.dsl.OrtusBuilder"
};

or
mapDSL("ortus","path.model.dsl.OrtusBuilder");
```

This will register a new injection DSL namespace called ortus that maps to that instantiation component `path.model.dsl.OrtusBuilder`. Here is a very simple DSL Builder:

```javascript
<cfcomponent implements="wirebox.system.ioc.dsl.IDSLBuilder" output="false">

    <---  init --->
    <cffunction name="init" output="false" access="public" returntype="any" hint="Configure the DSL for operation and returns itself" colddoc:generic="wirebox.system.ioc.dsl.IDSLBuilder">
        <cfargument name="injector" type="any" required="true" hint="The linked WireBox injector" colddoc:generic="wirebox.system.ioc.Injector"/>
        <cfscript>
            instance = { injector = arguments.injector };
            instance.log        = instance.injector.getLogBox().getLogger( this );

            return this;
        </cfscript>
    </cffunction>

    <---  process --->
    <cffunction name="process" output="false" access="public" returntype="any" hint="Process an incoming DSL definition and produce an object with it.">
        <cfargument name="definition" required="true" hint="The injection dsl definition structure to process. Keys: name, dsl"/>
        <cfargument name="targetObject" required="false" hint="The target object we are building the DSL dependency for."/>
        <cfscript>
            var thisType             = arguments.definition.dsl;
            var thisTypeLen         = listLen(thisType,":");
            var utilName             = "";

            // DSL stages
            switch(thisTypeLen){
                // Ortus
                case 1 : { return instance.injector.getInstance('ortusUtil'); }
                // Ortus:utility
                case 2 : {
                    utilName = getToken(thisType,2,":");
                    // Verify that cache exists
                    if( instance.injector.containsInstance( 'Ortus#utilName'# ) ){
                        return instance.injector.getInstance( 'Ortus#utilName#' );
                    }
                    else if( instance.log.canDebug() ){
                        instance.log.debug("Cannot find named ortus utility #utilName# using definition: #arguments.definition.toString()#");
                    }
                    break;
                }
            } // end level 2 main DSL
        </cfscript>
    </cffunction>

</cfcomponent>
```

As you can see from the sample, creating your own DSL builder is fairly easy. The benefits of a custom DSL builder is that you can very easily create and extend the injection DSL language to your own benefit and if you are funky enough, override the behavior of the internal DSL Namespaces.

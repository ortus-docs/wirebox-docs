# Scoping Process

The scoping process must be done by using some of the referenced injector's methods:

* `buildInstance(mapping, initArguments)`
* `autowire()`

These methods must be called sequentially in order to avoid circular reference locks. The first method `buildInstance` is used to construct and initialize an object instance. The autowire method is used then to process DI and AOP on the targeted object. Let's look at my Ortus Scope:

```javascript
<cfcomponent output="false" implements="wirebox.system.ioc.scopes.IScope" hint="I am the Ortus Scope of Scopes">

    <---  init --->
    <cffunction name="init" output="false" access="public" returntype="any" hint="Configure the scope for operation">
        <cfargument name="injector" type="any" required="true" hint="The linked WireBox injector" colddoc:generic="wirebox.system.ioc.Injector"/>
        <cfscript>
            instance = {
                injector = arguments.injector,
                ortus = {}
            };
            return this;
        </cfscript>
    </cffunction>

    <---  getFromScope --->
    <cffunction name="getFromScope" output="false" access="public" returntype="any" hint="Retrieve an object from scope or create it if not found in scope">
        <cfargument name="mapping"             type="any" required="true"  hint="The object mapping" colddoc:generic="wirebox.system.ioc.config.Mapping"/>
        <cfargument name="initArguments"     type="any" required="false" hint="The constructor structure of arguments to passthrough when initializing the instance" colddoc:generic="struct"/>
        <cfscript>
            var name = arguments.mapping.getName();
            if( structKeyExists(instance.ortus, name) ){
                return instance.ortus[name];
            }

            lock name="ortus.scope.#arguments.mapping.getName()#"{
                instance.ortus[name] = instance.injector.buildInstance( arguments.mapping, arguments.initArguments );
            }

            // wire it
            instance.injector.autowire(target=instance.ortus[name],mapping=arguments.mapping);

            // send it back
            return instance.ortus[name];
        </cfscript>
    </cffunction>

</cfcomponent>
```

> **Caution** Always make sure that you use the `buildInstance` method and then store the results in the scope before wiring is done to avoid endless loops errors.


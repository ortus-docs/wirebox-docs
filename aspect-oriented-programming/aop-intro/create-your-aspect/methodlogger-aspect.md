# MethodLogger Aspect

Here is my MethodLogger aspect that I will create:

```javascript
<cfcomponent output="false" implements="wirebox.system.aop.MethodInterceptor" hint="A simple interceptor that logs method calls and their results">

    <---  Dependencies --->
    <cfproperty name="log" inject="logbox:logger:{this}">

    <---  init --->
    <cffunction name="init" output="false" access="public" returntype="any" hint="Constructor">
        <cfargument name="logResults" type="boolean" required="false" default="true" hint="Do we log results or not?"/>
        <cfscript>
            instance = {
                logResults = arguments.logResults
            };

            return this;
        </cfscript>
    </cffunction>

    <---  invokeMethod --->
    <cffunction name="invokeMethod" output="false" access="public" returntype="any" hint="Invoke an AOP method invocation">
        <cfargument name="invocation" required="true" hint="The method invocation object: wirebox.system.aop.MethodInvocation">
        <cfscript>
            var refLocal = {};
            var debugString = "target: #arguments.invocation.getTargetName()#,method: #arguments.invocation.getMethod()#,arguments:#serializeJSON(arguments.invocation.getArgs())#";

            // log incoming call
            log.debug(debugString);

            // proceed execution
            refLocal.results = arguments.invocation.proceed();

            // result logging and returns
            if( structKeyExists(refLocal,"results") ){
                if( instance.logResults ){
                    log.debug("#debugString#, results:", refLocal.results);
                }
                return refLocal.results;
            }
        </cfscript>
    </cffunction>

</cfcomponent>
```

You can see that I do some DI via annotations:

```javascript
<---  Dependencies --->
<cfproperty name="log" inject="logbox:logger:{this}">
```

A normal constructor with one optional argument for logging results:

```javascript
<---  init --->
<cffunction name="init" output="false" access="public" returntype="any" hint="Constructor">
    <cfargument name="logResults" type="boolean" required="false" default="true" hint="Do we log results or not?"/>
    <cfscript>
        instance = {
            logResults = arguments.logResults
        };

        return this;
    </cfscript>
</cffunction>
```

And our invokeMethod implementation:

```javascript
<---  invokeMethod --->
<cffunction name="invokeMethod" output="false" access="public" returntype="any" hint="Invoke an AOP method invocation">
<cfargument name="invocation" required="true" hint="The method invocation object: wirebox.system.aop.MethodInvocation">
<cfscript>
    var refLocal = {};
    var debugString = "target: #arguments.invocation.getTargetName()#,method: #arguments.invocation.getMethod()#,arguments:#serializeJSON(arguments.invocation.getArgs())#";

    // log incoming call
    log.debug(debugString);

    // proceed execution
    refLocal.results = arguments.invocation.proceed();

    // result logging and returns
    if( structKeyExists(refLocal,"results") ){
        if( instance.logResults ){
            log.debug("#debugString#, results:", refLocal.results);
        }
        return refLocal.results;
    }
</cfscript>
</cffunction>
```

As you can see, the before advice part is what happens before the execution of the real method \(or more aspects\) occurrs. So everything before the call to `arguments.invocation.proceed()`:

```javascript
var refLocal = {};
var debugString = "target: #arguments.invocation.getTargetName()#,method: #arguments.invocation.getMethod()#,arguments:#serializeJSON(arguments.invocation.getArgs())#";

// log incoming call
log.debug(debugString);
```

Then we execute the real method or more aspects \(we do not do anything around the method call\):

```javascript
// proceed execution
refLocal.results = arguments.invocation.proceed();
```

Finally, we do the after advice part which happens after the method or other aspects fire and results are returned:

```javascript
// result logging and returns
if( structKeyExists(refLocal,"results") ){
    if( instance.logResults ){
        log.debug("#debugString#, results:", refLocal.results);
    }
    return refLocal.results;
}
```

That's it. I have succesfully created an aspect. What's next!


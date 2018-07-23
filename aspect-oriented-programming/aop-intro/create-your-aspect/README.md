# Create Your Aspect

Now that we have activated the AOP engine, let's build a simple method logger aspect that will intercept before our method is called and after our method is called. So if you remember your AOP dictionary terms, we will create an aspect that does a before and after advice on the method. Phew! To do this we must implement a CFC that WireBox AOP gives you as a template: `wirebox.system.aop.MethodInterceptor`. This CFC interface looks like this:

```javascript
<cfinterface hint="Our AOP Method Interceptor Interface">

    <---  invokeMethod --->
    <cffunction name="invokeMethod" output="false" access="public" returntype="any" hint="Invoke an AOP method invocation">
        <cfargument name="invocation" required="true" hint="The method invocation object: wirebox.system.ioc.aop.MethodInvocation">
    </cffunction>

</cfinterface>
```

This means, that we must create a CFC that implements the `invokeMethod` method with our own custom code. It also receives 1 argument called `invocation` that maps to a CFC called `wirebox.system.aop.MethodInvocation` that you can learn from our cool [API](http://www.coldbox.org/api).

Our approach to AOP is simplicity, therefore this `invokeMethod` implements the most powerful advice called around advice, so you will always do an around advice, but it will be up to your custom code to decide what it does before \(**beforeAdvice**\), around \(**aroundAdvice**\) and after \(**afterAdvice**\) the method call.

The other advantage of WireBox AOP aspects is that once they are registered with WireBox they act just like normal DI objects in WireBox, therefore you can apply any type of dependency injection to them.


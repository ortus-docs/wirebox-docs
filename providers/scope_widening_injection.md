# Scope Widening Injection

<img src="../images/scope_wideningInjection.jpg">

An object that is scoped into request, session, server, cachebox or application scopes and if wired into a persisted object will remain around even when this object has expired from the scope. This is called scope-widening injection and is a problem that must be addressed by NOT injecting them into persisted objects directly but by using WireBox's provider approach. This guarantees that the object's scope lifecycle will be maintained and your singleton or other persistent objects will be decoupled from the scope by accessing the target object via its provider.

For example, let's say you have a handler that wires in a user object that is scoped into session scope, but the handler itself is scoped as a singleton:

```javascript
component name="handler" singleton{

	property name="user" inject="id:user";
}

//user component
component name="user" scope="session"{
}
```

So when the handler is created and persisted as a singleton, the user object get's created, stored in session and also referenced into the lifecycle of the handler object. So now, if the user expires from session, the handler does not know about it, because all it knows it that a direct reference to that out of context object still remains. So if the user needed things in session to exist, this will now fail. This problem is much how hibernate and detached objects works. Objects are no longer in session, they are detached. This scope widening issue is resolved by NOT injecting the user object directly into the handler but by using a provider.

<img src="../images/scope_wideningInjectionSolution.jpg">
&rarr; Scope Widening Injection Solution: Object Providers

Below is my favorite approach to solving the issue which is by using provided methods:

```javascript
component name="handler" singleton{

	function getUser() provider="user"{}

}
```

That's it! My getUser() method will be replaced by WireBox with a proxy provider method that will request from the WireBox injector the user mapping instance.


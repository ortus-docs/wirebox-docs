# Virtual Provider Injection DSL

You can inject automatic object providers by using the provider injection DSL namespace. This will inject a WireBox provider class (`wirebox.system.ioc.Provider`) that follows our [Provider pattern](http://en.wikipedia.org/wiki/Provider_model) with one method on it: `get()` that will provide you with the requested mapped object. 

The difference between custom providers here is that WireBox will create a virtual provider object for you dynamically at runtime, configure it to retrieve a specific type of mapping and then use that for you. The **provider** namespace will take everything after it and evaluate it as either a named mapping or a full injection DSL string.

For example, `inject="provider:MyService"` will inject a provider of `MyService` objects, so it will look for a `MyService` ID in the binder. However, you can also get mega funky and do this: `inject="provider:logbox:logger:{this}"` and WireBox will create a provider of `logbox:logger:{this}`.

> **Important** Remember that the value of the provider can be a simple ID or a full injection DSL.

```javascript
// use the provider DSL namespace on a property
property name="searchCriteria" inject="provider:requestCriteria";

// use the provider DSL namespace on a constructor argument
function init(coolObjectProvider inject="provider:HardToConstructObject"){
	variables.coolObjectProvider = arguments.coolObjectProvider;
	return this;
}

// To use it
searchCriteria.get().getCriteria();
coolObjectProvider.get().executeSomeMethod();
```
<br>
That's it! You basically use the provider:{mapping} injection DSL to tell a property, setter or argument that you want a provider object instead of the real deal. This will allow you to delay construction of such object or avoid the nasty pitfall of scope widening injection.

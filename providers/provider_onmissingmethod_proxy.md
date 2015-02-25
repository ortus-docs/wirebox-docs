# Provider onMissingMethod Proxy

Thanks to our friend Brad Wood, we have a feature in our Providers that you can leverage its onMissngMethod() to proxy calls into the provided object itself. So let's say our provided object has a method called sayHello(), then with an injected provider you must do this:

```javascript
property name="chatter" inject="provider:Chat";

function useChatter(){
	return chatter.get().sayHello();
}
```
That is great, but you can proxy calls into the provider itself by doing this:

```javascript
property name="chatter" inject="provider:Chat";

function useChatter(){
	return chatter.sayHello();
}
```

The WireBox provider object (coldbox.system.ioc.Provider) has an onMissingMethod() function that will take all missing method calls and proxy them to the provided object. Now, this is great but be ready to lose on performance if you use this approach. That is the only caveat to this approach, is that you will be impacted by performance, not crazy, but try it.

# What's New With 5.0.0

This release is part of the ColdBox 5.0.0 upgrade and it is a major release. Below you will find the major areas of improvement for WireBox and the full release notes.

## Error Reporting

We have done greats strides in consistency of error reporting during the creation of objects and their wiring. We have also added countermeasures for **rogue** mappings that could bring entire applications down. You will now get more consistency and better error reporting overall.

## AOP Performance

AOP now performs in over 70% faster than previous implementations. In previous versions, we would create intermediate class files that would then be loaded and injected as part of the AOP proxies. This took time and not only that, it would create 1 stub per call to a method implementation. Our strategy worked but lacked performance. In 5.0.0 we completely re-architected the way we did method injection and stub creation. We now take md5 hashes of the source code to be injected and only created the stubs 1 per-lifetime. The improvements are drastic and amazing. Enjoy AOP and don't hold back!

## DI Performance

We have moved from an `instance` scope approach to a `variables` scope approach with accessors and mutators in 5.0.0 and yet again we benefit from CFML engine speed improvements. Again, thanks to the community for many pull requests.

## Virtual Inheritance

We have completely re-engineered virtual inheritance in 5.0.0 and it behaves eerily similar to traditional inheritance at the dynamic level. Not only do we cover public methods like we used to, but also private methods and object state. You can also leverage AOP with virtual inheritance now which was a limitation in the previous version.

We have also added the capability to inherit implicit getters and setters from parent classes.

## Listener Registration

You now can register listeners on-demand with WireBox via the `registerListener( listener )` method in the Injector.

## New `onLoad(), onShutdown()` Binder Callbacks

Any WireBox binder can now have two new callback methods `onLoad(), onShutdown()`. The `onLoad()` is called once WireBox has loaded with logging, caching, and the `configure()` on the binder has been called. You can use this for leveraging `mapDirectory()` calls which require the entire event system to be online or any other type of execution that leverages the entire machinery to be online.

The `onShutdown()` callback is a nice way to shutdown services as you see fit.

```java
function onLoad(){
    mapDirectory( "commandbox.commands" );
}
```

## Binder Is An Interceptor

The new WireBox Binder object is also an interceptor now. So you can create functions that listen to the entire DI/AOP process. Please see the [events sections](../../usage/wirebox-event-model/wirebox-events.md).

## Release Notes

### Bugs

* \[[WIREBOX-29](https://ortussolutions.atlassian.net/browse/WIREBOX-29)\] - Virtual inheritance breaks AOP on on base class methods.
* \[[WIREBOX-52](https://ortussolutions.atlassian.net/browse/WIREBOX-52)\] - Virtual Inheritance doesn't inherit variables-scoped properties
* \[[WIREBOX-63](https://ortussolutions.atlassian.net/browse/WIREBOX-63)\] - CFC's with same name don't get aliases picked up with mapDirectory\(\)
* \[[WIREBOX-64](https://ortussolutions.atlassian.net/browse/WIREBOX-64)\] - Illusive double id exception when race conditions

### New Features

* \[[WIREBOX-58](https://ortussolutions.atlassian.net/browse/WIREBOX-58)\] - Allow new listeners added to the Binder to also be registered right away, especially from modules
* \[[WIREBOX-62](https://ortussolutions.atlassian.net/browse/WIREBOX-62)\] - New request context dsl injection -&gt; coldbox:requestContext
* \[[WIREBOX-67](https://ortussolutions.atlassian.net/browse/WIREBOX-67)\] - New coldbox dsl element =&gt; coldbox:router to retrieve the application's router object.
* \[[WIREBOX-68](https://ortussolutions.atlassian.net/browse/WIREBOX-68)\] - Virtual Inheritance now copies over properties and private functions with generic accessors
* \[[WIREBOX-69](https://ortussolutions.atlassian.net/browse/WIREBOX-69)\] - Module Injection Shortcut when the inject annotation is @moduleAdress
* \[[WIREBOX-70](https://ortussolutions.atlassian.net/browse/WIREBOX-70)\] - Add a new `onLoad()` method interceptor for WireBox configuration binder
* \[[WIREBOX-72](https://ortussolutions.atlassian.net/browse/WIREBOX-72)\] - Make the Binder also an interceptor
* \[[WIREBOX-73](https://ortussolutions.atlassian.net/browse/WIREBOX-73)\] -         Add a new `onShutdown()` method interceptor for WireBox configuration binder

### Improvements

* \[[WIREBOX-28](https://ortussolutions.atlassian.net/browse/WIREBOX-28)\] - Improve errors while building depenencies
* \[[WIREBOX-34](https://ortussolutions.atlassian.net/browse/WIREBOX-34)\] - Improve AOP binding by caching temp files
* \[[WIREBOX-59](https://ortussolutions.atlassian.net/browse/WIREBOX-59)\] - Throw error on non-existent coldbox DSL
* \[[WIREBOX-65](https://ortussolutions.atlassian.net/browse/WIREBOX-65)\] - Increase Wirebox performance by scoping variables
* \[[WIREBOX-66](https://ortussolutions.atlassian.net/browse/WIREBOX-66)\] - Complete refactoring of wirebox scopes/DSL to script and direct scope usage
* \[[WIREBOX-71](https://ortussolutions.atlassian.net/browse/WIREBOX-71)\] - Ability to cache metadata in CacheBox 


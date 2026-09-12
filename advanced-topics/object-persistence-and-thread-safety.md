# Object Persistence & Thread Safety

While the injector can help in many ways to secure the creation of your objects, it is ultimately up to you to create code that is both thread safe and tested. It is always a great idea to design your objects without the injector in mind for threading and concurrency.

**Dependency Injection** is not a silver bullet, but a tool to relieve object creation and not to relieve the burden of good object design. Thread safety is much more complex and can be compromised when using persistent scopes like singleton, session, server, application and cachebox, as more than one thread will be trying to access your code and dependencies.

**The only guarantee, by default, the injector can provide is the constructor and constructor dependency creation to be completely locked**.  This is the default behavior of the majority of DI engines, including WireBox. However, setter and property injections are not guaranteed to be thread safe unless you mark the class as thread safe. This is done in order to allow for circular dependencies in the object graph. If you mark an object as thread safe, then the injector will lock the entire process of constructing and wiring the object, but it will not be able to support circular dependencies unless you use providers. (See [Providers Section](providers/README.md) )

The following object is to be guaranteed to be locked when created and wired with dependencies:

{% tabs %}

{% tab title="BoxLang" %}
```boxlang
class{

     /**
     * Constructor injection is guaranteed to be thread safe and locked by the injector. However, setter and property injections are not guaranteed to be thread safe unless you mark the component as thread safe. (See below)
     */
    @log.inject( "logbox:logger:{this}" )
    @dao.inject( "id:MyDAO" )
     function init( required log, required dao ){
          variables.log = arguments.log;
          variables.dao = arguments.dao;
          return this;
     }

}
```
{% endtab %}

{% tab title="CFML" %}
```cfscript
component{

     /**
      * Constructor injection is guaranteed to be thread safe and locked by the injector. However, setter and property injections are not guaranteed to be thread safe unless you mark the component as thread safe. (See below)
     */
     function init( required log, required dao ) log.inject="logbox:logger:{this}" dao.inject="id:MyDAO" {
          variables.log = arguments.log;
          variables.dao = arguments.dao;
          return this;
     }

}
```
{% endtab %}

{% endtabs %}

An example of a flawed object could be the following:

{% tabs %}

{% tab title="BoxLang" %}
```boxlang
class{

     @inject( "id:MyDAO" )
     property name="dao";

     @inject( "logbox:logger:{this}" )
     property name="log";

     function init(){
          return this;
     }
}
```
{% endtab %}

{% tab title="CFML" %}
```cfscript
component{

     property name="dao" inject="id:MyDAO";
     property name="log" inject="logbox:logger:{this}";

     function init(){
          return this;
     }
}
```
{% endtab %}

{% endtabs %}

Why is this object flawed? It is flawed because the majority of DI engines, including WireBox, will lock for constructing the object and its constructor arguments. However, once it is constructed, it will store the object in the persistence scope of choice in order to satisfy the potential of circular dependencies in the object graph. After it is placed in the storage, the DI engines will wire up setter and property mixin injections and WireBox's `onDiComplete()` method. With this normal approach, the wiring of dependencies and `onDiComplete()` have the potential of mixups or missing dependencies due to concurrency. This is a normal side-effect and risk that developers take due that Java makes no guarantees that any thread other than the one that set its dependencies will see the dependencies. The memory between threads is not final or immutable so properties can enter an altered state.

> "The subtle reason has to do with the way Java Virtual Machines (JVM) are designed to manage threads. Threads may keep local, cached copies of non-volatile fields that can quickly get out of sync with one another unless they are synchronized correctly." \
> From Dependency Injection by Dhanji R. Prasanna
> **Note** This side effect of concurrency will only occur on objects that are singletons or persisted in scopes like session, server, application, server or cachebox. It does not affect transient or request scoped objects.

WireBox, can help you lock and provide thread safety to setter and property injections by providing you with the `ThreadSafe` annotation or our binder `threadSafe()` tagging method. So if we wanted to make the last example thread safe for property and setter wiring then we would do the following:

{% tabs %}

{% tab title="BoxLang" %}
```boxlang
@threadSafe
class{

     @inject( "id:MyDAO" )
     property name="dao";

     @inject( "logbox:logger:{this}" )
     property name="log";

     function init(){
          return this;
     }
}
```
{% endtab %}

{% tab title="CFML" %}
```cfscript
component threadsafe{

     property name="dao" inject="id:MyDAO";
     property name="log" inject="logbox:logger:{this}";

     function init(){
          return this;
     }
}
```
{% endtab %}

{% endtabs %}

Or you can map the object as thread safe via the binder:

```js
// or you can bind it as a thread safe component
map("MyObject").to("path.model.MyObject").asSingleton().threadSafe();
```

> **Note** All objects are marked as non thread safe for dependency wiring by default in order to allow for circular dependencies. Please note that if you mark an object as `threadSafe`, then it will not be able to support circular dependencies unless it uses WireBox providers. ( See [Providers Section](https://github.com/ortus/wirebox-documentation/tree/b9a6ae3e91f7dcb74ec7e900e27243e19824cf27/object_persistence_&_thread_safety/providers/README.md) )

Our `threadSafe` annotation and binder tagging property will allow for these objects to be completely locked and synchronized for object creation, wiring and `onDiComplete()`. However, circular dependencies will now fail as persistence cannot be guaranteed for the setter or property dependencies. However, since WireBox is so awesome, you can still use circular dependencies by wiring instead our object providers. (Please see providers section). In conclusion, constructing and designing a CFC that is thread safe is often a very arduous process. It is also very difficult to test and recreate threading issues in your objects and applications. So don't feel bad, as even the best of us can get into some nasty wormholes when dealing with concurrency and thread safety. However, always try to design for as much concurrency as possible and test test test!

## Transient Request Persistence

This feature is one of the most impactful for applications that leverage DI on transient objects, especially ORM-related applications. WireBox caches the signatures of the injections and delegations for you, so they are only computed once per instance type per request. This yields dramatic performance improvements (over 585% in real-world ORM-heavy apps). The best part: it is on by default. Install and run it.

### Configuration

If this is not for you or it causes issues in your system, disable it globally via the WireBox binder:

```javascript
// Config DSL
wirebox = {
     transientInjectionCache : false
};

// Binder call
binder.transientInjectionCache( false );
```

You can also disable the cache on a per-CFC basis:

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class transientCache="false"{
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component transientCache="false"{
}
```
{% endtab %}
{% endtabs %}

### Known Issues

Because the cache reuses injection and delegation results per Class definition, injected transients can effectively behave like singletons within the request. If you inject transients that must remain unique per instance, use one of the following approaches:

1. Disable the cache entirely (heavy-handed approach)
2. Disable the cache on that specific Class via `transientCache` (surgical approach)
3. Inject the dependency as a provider (ninja approach)
4. Make the property lazy and build it on demand (Jedi approach)

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class name="Transient" transientCache="false"{
     // This will become a singleton within the request if caching is enabled
     property name="transient2" inject="t2";
     // Provider injection
     property name="transient2" inject="provider:t2";
     // Lazy property
     property name="transient2" lazy;

     function buildTransient2(){
          return variables.wirebox.getInstance( "t2" );
     }
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component name="Transient" transientCache="false"{
     // This will become a singleton within the request if caching is enabled
     property name="transient2" inject="t2";
     // Provider injection
     property name="transient2" inject="provider:t2";
     // Lazy property
     property name="transient2" lazy;

     function buildTransient2(){
          return variables.wirebox.getInstance( "t2" );
     }
}
```
{% endtab %}
{% endtabs %}
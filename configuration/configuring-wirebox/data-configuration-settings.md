# Data Configuration Settings

In the `configure()` method you can create a structure called `wirebox` in the `variables` scope that will hold the configuration data for WireBox. You can configure WireBox for operation using these structures or via [programmatic method calls](programmatic-configuration.md).

```javascript
/**
* Configure WireBox
*/
function configure(){

    // The WireBox configuration structure DSL
    wireBox = {

        // LogBox Config: instantiation path
        logBoxConfig = "wirebox.system.ioc.config.LogBox",

        // CacheBox
        cacheBox = { enabled = true },

        // Scope registration, automatically register a wirebox injector instance on any CF scope
        // By default it registeres itself on application scope
        scopeRegistration = {
            enabled = true,
            scope   = "application", // server, cluster, session, application
            key        = "wireBox"
        },

        // DSL Namespace registrations
        customDSL = {
            // namespace = "mapping name"
        },

        // Custom Storage Scopes
        customScopes = {
            // annotationName = "mapping name"
        },

        // Package scan locations
        scanLocations = [],

        // Stop Recursions
        stopRecursions = [],

        // Parent Injector to assign to the configured injector, this must be an object reference
        parentInjector = "",

        // Register all event listeners here, they are created in the specified order
        listeners = [
            // { class="", name="", properties={} }
        ]
    };

    // Map Bindings below
}
```

{% hint style="info" %}
Please note that it is completely optional to use the implicit structure configuration. You can use the programmatic methods instead. Each configuration key has the same method in the binder for programmatic configuration.
{% endhint %}

## logBoxConfig

The path to the LogBox Configuration object to use. By default it uses the one displayed below. If you are using WireBox within a ColdBox application, the LogBox configuration is taken from the ColdBox application.

```javascript
wirebox.logBoxConfig = "wirebox.system.ioc.config.LogBox";
```

## cachebox

If you are using WireBox within a ColdBox application this setting is ignored and it will use the ColdBox application's CacheBox configuration. The following are the keys for this configuration structure:

```javascript
wirebox.cacheBox = {
    // Activate the CacheBox DSL and caching
    enabled = false,
    // An optional configuration file to use for loading CacheBox
    configFile = "coldbox.system.ioc.config.CacheBox",
    // A reference to an already instantiated CacheBox CacheFactory, instead of building one
    cacheFactory = "",
    //A class path namespace to use to create CacheBox: Default=coldbox.system.cache or wirebox.system.cache
    classNamespace = ""
};
```

## scopeRegistration

This structure tells WireBox how to leach itself into any ColdFusion scope when initialized instead of you placing it in the scope.

```javascript
wirebox.scopeRegistration = {
    // activate scope registration
    enabled = true,
    // The CF scope to place the WireBox injector on
    scope   = "application",
    // The key used to store it in the scope
    key        = "wireBox"
};
```

{% hint style="danger" %}
**Caution** Scope registration must be enabled in order for Providers to work.
{% endhint %}

## customDSL

Please refer to the [Custom DSL](../../extending-wirebox/custom-dsl/) section to find out more about custom DSLs, the following are just the way you declare them:

```javascript
wirebox.customDSL = {
    // The value of the DSL Namespace is the instantiation path
    // of the DSL Namespace builder that implements wirebox.system.ioc.DSL.IDSLBuilder
    cool = "my.path.CoolDSLBuilder",
    funkyBox = "my.funky.DSLBuilder"
};
```

## customScopes

Please refer to the [Custom scopes](../../extending-wirebox/custom-scopes/) section to find out more about custom scopes, the following are just the way you declare them:

```javascript
wirebox.customScopes = {
    // The value of the instantiation path of the custom scope
    // that implements coldbox.system.ioc.scopes.IScope.
    // The name of the scope will be used when registered
    // the scope annotation.
    CoolSingletons = "my.path.SingletonScope",
    FunkyTransaction = "my.funky.Transaction"
};
```

## scanLocations

The instantiation paths that this Injector will have registered to do object locations in order. So if you request an object called `Service` and no mapping has been configured for it, then WireBox will search all these scan locations for a `Service.cfc` in the specified order. The last lookup is the no namespace lookup which basically represents a `createObject("component","Service")` call. If you are using WireBox within a ColdBox application, ColdBox will register the `models` convention folder for you.

```javascript
wirebox.scanLocations = ["models","com","org.majano"];
```

{% hint style="warning" %}
Please note that order of declaration is the same as order of lookup, so it really matters. Also note that this setting only makes sense if you do not like to create mappings for objects and you just want WireBox to discover them for you.
{% endhint %}

## stopRecursions

This is an array of class path's that WireBox will use to stop recursion on any object graph that has inheritance when looking for dependencies.

```javascript
wirebox.stopRecursions = [ "transfer.com.TransferDecorator", "coldbox.system.EventHandler" ];
```

## parentInjector

This setting is actually a reference to another parent injector you would like this injector to set as its parent injector. Now say this sentence 10 times without hiccuping.

```javascript
wirebox.parentInjector = application.coolInjector;
// or
wirebox.parentInjector = new coldbox.system.ioc.Injector( "old.legacy.binder" );
```

## listeners

This section only shows you how to register WireBox listeners, so please refer to the object life cycle events section for more information. This setting is an array of listener structure definitions that WireBox's event manager will use when broadcasting object life cycle events.

```javascript
wirebox.listeners = [
    {
        // The path to the listener
        class="path.to.CFC",
        // A unique name for the listener
        name="UniqueName",
        // A structure of name-value pairs for configuring this interceptor
        properties = {}
    }
    {class="my.AOPTracker"},
    {class="annotationTransactioner",properties={target='*'} },
    {class="Timer", name="CoolTimer"}
];
```

{% hint style="danger" %}
**Caution** Please note that order of declaration is the same as order of execution, so it really matters, just like ColdBox Interceptors. Please note that if you are using WireBox within a ColdBox application, you can also register listeners as interceptors in your ColdBox configuration file.
{% endhint %}

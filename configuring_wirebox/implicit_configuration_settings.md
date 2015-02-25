# Implicit Configuration Settings

In the `configure()` method you can create a structure called `wirebox` in the `variables` scope that will hold the configuration data for WireBox. 

```
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
			key		= "wireBox"
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


> **Info** Please note that it is completely optional to use the implicit structure configuration. You can use the programmatic methods instead. Each configuration key has the same method in the binder for programmatic configuration.

## logBoxConfig

The path to the LogBox Configuration object to use.  By default it uses the one displayed below.  If you are using WireBox within a ColdBox application, the LogBox configuration is taken from the ColdBox application.

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

```
wirebox.scopeRegistration = {
    // activate scope registration
	enabled = true,
	// The CF scope to place the WireBox injector on
	scope   = "application",
	// The key used to store it in the scope
	key		= "wireBox"
};
```

> **Important** Scope registration must be enabled in order for Providers to work.

## customDSL

Please refer to the [Custom DSL](../custom_dsl_builder/README.md) section to find out more about custom DSLs, the following are just the way you declare them:


```javascript
wirebox.customDSL = {
    // The value of the DSL Namespace is the instantiation path 
    // of the DSL Namespace builder that implements wirebox.system.ioc.DSL.IDSLBuilder
	cool = "my.path.CoolDSLBuilder",
	funkyBox = "my.funky.DSLBuilder"
};
```

## customScopes
Please refer to the [Custom scopes](../custom_scopes/README.md) section to find out more about custom scopes, the following are just the way you declare them:

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

> ** Note** Please note that order of declaration is the same as order of lookup, so it really matters. Also note that this setting only makes sense if you do not like to create mappings for objects and you just want WireBox to discover them for you. 

```javascript
wirebox.scanLocations = ["model","transfer.com","org.majano"];
```
## stopRecursions
This is an array of class path's that WireBox will use to stop recursion on any object graph that has inheritance when looking for dependencies. For example, let's say your object inherits from transfer.com.TransferDecorator, but you don't want WireBox to go past that inheritance class when looking for DI data, then you would add transfer.com.TransferDecorator to this setting.

```javascript
wirebox.stopRecursions = ["transfer.com.TransferDecorator","coldbox.system.EventHandler"];
```
<h4 style="color:blue">parentInjector</h4>
This setting is actually a reference to another parent injector you would like this injector to set as its parent injector. Now say this sentence 10 times without hiccuping.

```javascript
wirebox.parentInjector = application.coolInjector;
// or
wirebox.parentInjector = createObject("component","coldbox.system.ioc.Injector").init("old.legacy.binder");
```
<h4 style="color:blue">listeners</h4>
This section only shows you how to register WireBox listeners, so please refer to the object life cycle events section for more information. This setting is an array of listener structure definitions that WireBox's event manager will use when broadcasting object life cycle events. Each interceptor structure definition has the following keys:

| Key | Type | Required | Default | Description |
| -- | -- | -- | -- | -- |
| class | class path  | true  | --- | The instantiation class path of the listener |
| name | string | false | Name of the CFC  | The unique name of this listener when registered in our event manager. We recommend setting one up as best practice, else the name of the CFC file will be used instead. This setting is great for registering the same class with different configurations. |
| properties | struct | false | {} | A structure of configuration data for this listener |

<br>
<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="13%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Important: Please note that order of declaration is the same as order of execution, so it really matters, just like ColdBox Interceptors. Please note that if you are using WireBox within a ColdBox application, you can also register listeners as [interceptors](http://wiki.coldbox.org/wiki/Interceptors.cfm) in your ColdBox configuration file.  </b></p>
<div style="clear:both"></div>
</div>
<br>

```javascript
wirebox.listeners = [
	{class="my.AOPTracker"},
	{class="annotationTransactioner",properties={target='*'} },
	{class="Timer", name="CoolTimer"}
];
```



# Configuring WireBox

1. Create a simple configuration CFC that has a `configure( binder )` method that accepts a WireBox configuration binder object
```javascript
component{
	function configure(required binder){

	}
}
```
2. Create a configuration CFC that extends the WireBox configuration object: `coldbox.system.ioc.config.Binder` and has a `configure()` method.
```javascript
component extends="coldbox.system.ioc.config.Binder"{
	function configure(){

	}
}
```

> **Info** The latter approach will be less verbose when talking to the mapping DSL the Binder object exposes. However, both are fully functional and matter of preference.

From the `configure()` method you will be able to interact with the Binder methods or creating implicit DSL structures in order to configure WireBox for operation and also to create object mappings.

> **Info** Please also note that the Binder itself has a reference to the current Injector it belongs to (`getInjector()`).






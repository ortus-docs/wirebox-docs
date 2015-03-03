# WireBox Configuration

The configuration binder has the same methods as the implicit structures that can be used to configure WireBox for operation:


|Method Signature|Description|
|--|--|
|<b>cacheBox</b>([configFile],[cacheFactory],[enabled],[classNamespace])|The method used to configure the injector's CacheBox integration. <b>Ignored in an application context|
|listener</b>(class,[properties],[name])|The method used to register a new listener within the injector's event manager|
|logBoxConfig</b>(config)|The method used to tell the injector which <a href="wiki/LogBox.cfm">LogBox</a> configuration file to use for logging operations. <b>Ignored in an application context|
|<b>mapDSL</b>(namespace,path)|The method used to register a new DSL annotation namespace with a DSL Builder object|
|<b>mapScope</b>(annotation,path)|The method used to register a new custom scope in this injector|
|<b>parentInjector</b>(injector)|Register a CFC reference to be the parent injector for the configuring injector|
|<b>removeScanLocations</b>(locations)|A method used to remove one or a list (array) of scan locations from the configuration binder|
|<b>reset</b>()|Reset the entire configuration binder to factory defaults|
|<b>scanLocations</b>(locations)| A method used to add one or a list (array) of scan locations to the configuration binder. If a path already exists it will not be appended again.|
|<b>scopeRegistration</b>(enabled,scope,key)|This method is used to tell the Injector if it should auto-register itself in any ColdFusion scope automatically|
|<b>stopRecursions</b>(classes)|A method used to register one or a list (array) of class paths the injector will look out for when discovering DI metadata. If these classes are found in the inheritance chain of an object, the injector will not process that inherited chain|

```js
	logBoxConfig("config.LogBox")
	.scanLocations( getAppMappig() & ".includes.models" )
	.stopRecursions( "model.BaseService,model.BaseModel" )
	.mapScope( "Ortus", "model.scopes.Ortus" );
```

# Programmatic Configuration

Instead of declaring data structures you can use the methods in the binder to configure WireBox for operation. All methods return an instance of the binder so you can concatenate methods.

| Method Signature | Description |
| --- | --- |
| **cacheBox**\(\[configFile\],\[cacheFactory\],\[enabled\],\[classNamespace\]\) | The method used to configure the injector's CacheBox integration. Ignored in an application context |
| **listener**&lt;/b&gt;\(class,\[properties\],\[name\]\) | The method used to register a new listener within the injector's event manager |
| **logBoxConfig**&lt;/b&gt;\(config\) | The method used to tell the injector which [LogBox](https://github.com/ortus/wirebox-documentation/tree/b9a6ae3e91f7dcb74ec7e900e27243e19824cf27/mapping_dsl/wiki/LogBox.cfm) configuration file to use for logging operations. Ignored in an application context |
| **mapDSL**\(namespace,path\) | The method used to register a new DSL annotation namespace with a DSL Builder object |
| **mapScope**\(annotation,path\) | The method used to register a new custom scope in this injector |
| **parentInjector**\(injector\) | Register a CFC reference to be the parent injector for the configuring injector |
| **removeScanLocations**\(locations\) | A method used to remove one or a list \(array\) of scan locations from the configuration binder |
| **reset**\(\) | Reset the entire configuration binder to factory defaults |
| **scanLocations**\(locations\) | A method used to add one or a list \(array\) of scan locations to the configuration binder. If a path already exists it will not be appended again. |
| **scopeRegistration**\(enabled,scope,key\) | This method is used to tell the Injector if it should auto-register itself in any ColdFusion scope automatically |
| **stopRecursions**\(classes\) | A method used to register one or a list \(array\) of class paths the injector will look out for when discovering DI metadata. If these classes are found in the inheritance chain of an object, the injector will not process that inherited chain |

```javascript
logBoxConfig( "config.LogBox" )
    .scanLocations( getAppMappig() & ".includes.models" )
    .stopRecursions( "model.BaseService,model.BaseModel" )
    .mapScope( "Ortus", "model.scopes.Ortus" );
```
# WireBox Configuration

The configuration binder has the same methods as the implicit structures that can be used to configure WireBox for operation:

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Method Signature</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>cacheBox</b>([configFile],[cacheFactory],[enabled],[classNamespace]) </td>
<td>The method used to configure the injector's CacheBox integration. <b>Ignored in an application context</b></td></tr>
<tr>
<td><b>listener</b>(class,[properties],[name]) </td>
<td>The method used to register a new listener within the injector's event manager.</td></tr>
<tr>
<td><b>logBoxConfig</b>(config) </td>
<td>The method used to tell the injector which <a href="wiki/LogBox.cfm">LogBox</a> configuration file to use for logging operations. <b>Ignored in an application context</b></td></tr>
<tr>
<td><b>mapDSL</b>(namespace,path) </td>
<td>The method used to register a new DSL annotation namespace with a DSL Builder object.</td></tr>
<tr>
<td><b>mapScope</b>(annotation,path) </td>
<td>The method used to register a new custom scope in this injector.</td></tr>
<tr>
<td><b>parentInjector</b>(injector) </td>
<td>Register a CFC reference to be the parent injector for the configuring injector</td></tr>
<tr>
<td><b>removeScanLocations</b>(locations) </td>
<td>A method used to remove one or a list (array) of scan locations from the configuration binder</td></tr>
<tr>
<td><b>reset</b>() </td>
<td>Reset the entire configuration binder to factory defaults</td></tr>
<tr>
<td><b>scanLocations</b>(locations) </td>
<td>A method used to add one or a list (array) of scan locations to the configuration binder. If a path already exists it will not be appended again.</td></tr>
<tr>
<td><b>scopeRegistration</b>(enabled,scope,key) </td>
<td>This method is used to tell the Injector if it should auto-register itself in any ColdFusion scope automatically.</td></tr>
<tr>
<td><b>stopRecursions</b>(classes) </td>
<td>A method used to register one or a list (array) of class paths the injector will look out for when discovering DI metadata. If these classes are found in the inheritance chain of an object, the injector will not process that inherited chain.</td></tr></tbody></table>

```javascript
	logBoxConfig("config.LogBox")
	.scanLocations( getAppMappig() & ".includes.models" )
	.stopRecursions( "model.BaseService,model.BaseModel" )
	.mapScope( "Ortus", "model.scopes.Ortus" );
```

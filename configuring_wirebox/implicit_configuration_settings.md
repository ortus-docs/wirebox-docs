# Implicit Configuration Settings

In this configure() method you can create a structure called wirebox in the variables scope that will hold the configuration data for WireBox. The following are the keys you can create in this structure:

<table>
    <tr>
        <th>Key</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Desecription</th>
    <tr>
    <tr>
        <td>logBoxConfig</td>
        <td>instantiation or xml path </td>
        <td>false</td>
        <td>coldbox.system.ioc.config.LogBox </td>
        <td>The LogBox configuration to use when logging. If you are within a ColdBox application context, this value is ignored.</td>
    <tr>
    <tr>
        <td>cacheBox </td>
        <td>struct</td>
        <td>false</td>
        <td>{enabled=false} </td>
        <td>A structure that defines the tight integration between WireBox and CacheBox (explained below). If you are within a ColdBox application context, this value is ignored.</td>
    <tr>
    <tr>
        <td>scopeRegistration </td>
        <td>struct</td>
        <td>false</td>
        <td>{enabled=true,scope="application",key="wirebox"} </td>
        <td>A structure that tells WireBox to register itself into ANY ColdFusion scope once instantiated. By default, each injector get's loaded into application scope with a key of wireBox, which we encourage you to modify.</td>
    <tr>
    <tr>
        <td>customDSL </td>
        <td>struct</td>
        <td>false</td>
        <td>{}</td>
        <td>A structure where you will register your own DSL Namespace implementations. Please refer to our Custom DSL section.</td>
    <tr>
    <tr>
        <td>customScopes </td>
        <td>struct</td>
        <td>false</td>
        <td>{}</td>
        <td>A structure where you will register your own object scope implementations. Please refer to our Custom Scopes section.</td>
    <tr>
    <tr>
        <td>scanLocations</td>
        <td>array</td>
        <td>false</td>
        <td>[]</td>
        <td>An array of instantiation locations WireBox will use (in order) when searching for objects when they are requested by convention.</td>
    <tr>
    <tr>
        <td>stopRecursions</td>
        <td>array</td>
        <td>false </td>
        <td>[]</td>
        <td>An array of class paths that WireBox will detect when inspecting objects for dependencies and STOP the inspection when doing inheritance recursion.</td>
    <tr>
    <tr>
        <td>parentInjector</td>
        <td>object</td>
        <td>false </td>
        <td>---</td>
        <td>The actual instance to a parent injector you would like to configure this injector with.</td>
    <tr>
    <tr>
        <td>listeners</td>
        <td>array of structs</td>
        <td>false</td>
        <td>---</td>
        <td>A array of listener definitions that will be registered with this injector and listen to object life cycle events.</td>
    <tr>
</table>

<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="12%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Please note that it is completely optional to use the implicit structure configuration. You can use the programmatic methods instead. Each configuration key has the same method in the binder for programmatic configuration. </b></p>
<div style="clear:both"></div>
</div>

<h4 style="color:blue">logBoxConfig</h4>

```javascript
wirebox.logBoxConfig = "coldbox.system.ioc.config.LogBox";
```

<h4 style="color:blue">cachebox</h4>

If you are using WireBox within a ColdBox application this setting is ignored. The following are the keys for this configuration structure:

| Key | Type | Required | Default | Description |
| -- | -- | -- | -- | -- |
| enabled | boolean |boolean | boolean | Enables [CacheBox](http://wiki.coldbox.org/wiki/CacheBox.cfm) integration |
| configFile | config path  | false  |coldbox.system.ioc.config.CacheBox |The [CacheBox](http://wiki.coldbox.org/wiki/CacheBox.cfm) configuration file to use when creating CacheBox|
| cacheFactory  | object | false |--- | A reference to an already instantiated CacheBox factory to use with this Injector |
| classNamespace | class path  | false | coldbox.system.cache  |The default namespace location of CacheBox. If using the standalone version of CacheBox you most likely will change this to cachebox.system.cache, else ignore this setting. |

```javascript
wirebox.cacheBox = {
	enabled = false,
	configFile = "coldbox.system.ioc.config.CacheBox", //An optional configuration file to use for loading CacheBox
	cacheFactory = "", //A reference to an already instantiated CacheBox CacheFactory
	classNamespace = "" //A class path namespace to use to create CacheBox: Default=coldbox.system.cache or wirebox.system.cache
};
```

<h4 style="color:blue">scopeRegistration</h4>
This structure tells WireBox how to leach itself into any ColdFusion scope when initialized.

<table>
    <tr>
        <th>Kry</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>enabled</td>
        <td>boolean</td>
        <td>false</td>
        <td>true</td>
        <td>Enables scope registration</td>
    </tr>
    <tr>
        <td>scope</td>
        <td>CF Scope</td>
        <td>true</td>
        <td>application</td>
        <td>The ColdFusion scope</td>
    </tr>
    <tr>
        <td>key</td>
        <td>string</td>
        <td>true</td>
        <td>wirebox</td>
        <td>The key to use in the ColdFusion scope when registering</td>
    </tr>
</table>

```javascript
wirebox.scopeRegistration = {
	enabled = true,
	scope   = "application", // server, cluster, session, application
	key		= "wireBox"
};
```
<h4 style="color:blue">customDSL</h4>

Please refer to the Custom DSL section to find out more about custom DSLs, the following are just the way you declare them:

<table>
    <tr>
        <th>Key</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>{DSLNamespace}</td>
        <td>string</td>
        <td>true</td>
        <td>---</td>
        <td>The value of the DSL Namespace is the instantiation path of the DSL Namespace builder that implements coldbox.system.ioc.DSL.IDSLBuilder</td>
    </tr>
</table>

```javascript
wirebox.customDSL = {
	cool = "my.path.CoolDSLBuilder",
	funkyBox = "my.funky.DSLBuilder"
};
```

<h4 style="color:blue">customScopes</h4>
Please refer to the Custom scopes section to find out more about custom scopes, the following are just the way you declare them:

<table>
    <tr>
        <th>Key</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>{ScopeName}</td>
        <td>string</td>
        <td>true</td>
        <td>---</td>
        <td>The value of the instantiation path of the custom scope that implements coldbox.system.ioc.scopes.IScope. The name of the scope will be used when registered the scope annotation.</td>
    </tr>
</table>
```javascript
wirebox.customScopes = {
	CoolSingletons = "my.path.SingletonScope",
	FunkyTransaction = "my.funky.Transaction"
};
```

<h4 style="color:blue">scanLocations</h4>
The instantiation paths that this Injector will have registered to do object locations in order. So if you request an object called Service and no mapping has been configured for it, then WireBox will search all these scan locations for a Service.cfc in the specified order. The last lookup is the no namespace lookup which basically represents a createObject("component","Service") call. If you are using WireBox within a ColdBox application, ColdBox will register the models convention folder for you and also whenever a ColdBox module is activated, that module's model convention folder will be added here too.
<br>
<br>
<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="13%" style="float:left;margin-top:10px"><p style="margin:12px"><b> Note:
Important: Please note that order of declaration is the same as order of lookup, so it really matters. Also note that this setting only makes sense if you do not like to create mappings for objects and you just want WireBox to discover them for you. </b></p>
<div style="clear:both"></div>
</div>
<br>

```javascript
wirebox.scanLocations = ["model","transfer.com","org.majano"];
```
<h4 style="color:blue">stopRecursions</h4>
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



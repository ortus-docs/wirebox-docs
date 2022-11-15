# Configuring WireBox

When using WireBox inside of ColdBox, the binder CFC is located by convention in `/config/WireBox.cfc`.  When using WireBox outside of ColdBox, you can create a binder CFC anywhere with any name using one of these two methods:

1. Create a configuration CFC that extends the WireBox configuration object: `coldbox.system.ioc.config.Binder` and has a `configure()` method.

```javascript
component extends="coldbox.system.ioc.config.Binder"{

    function configure(){

    }

    function onLoad(){

    }

    function onShutdown(){

    }
}
```

2\. Or create a simple configuration CFC that has a `configure( binder )` method that accepts a WireBox configuration binder object

```javascript
component{

 function configure(required binder){

 }

 function onLoad(){

 }

 function onShutdown(){

 }

}
```

{% hint style="info" %}
The latter approach will be less verbose when talking to the mapping DSL the Binder object exposes. However, both are fully functional and matter of preference.
{% endhint %}

From the `configure()` method you will be able to interact with the Binder methods or creating implicit DSL structures in order to configure WireBox for operation and also to create object mappings. From the `onLoad()` method you can also use it for mappings with main distinction that the WireBox machinery is now online (logging, events, caching, etc). This is necessary for leveraging `mapDirectory()` calls.

{% hint style="info" %}
Please also note that the Binder itself has a reference to the current Injector it belongs to (`getInjector()`).
{% endhint %}

When you instantiate the Wirebox injector, pass either the CFC path to your binder CFC or an instance of the CFC.

```javascript
new wirebox.system.ioc.Injector( 'path.to.my.Binder' );
// or
var oBinder = createObject( 'path.to.my.Binder' );
new wirebox.system.ioc.Injector( oBinder );
```

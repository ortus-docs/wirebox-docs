# Configuring WireBox

When using WireBox inside of ColdBox, the binder CFC is located by convention in `/config/WireBox.cfc` (or `/config/WireBox.bx` for BoxLang applications). When using WireBox outside of ColdBox, you can create a binder anywhere with any name using one of these two approaches:

**1. Extend the WireBox Binder** — create a configuration class that extends `coldbox.system.ioc.config.Binder` and implements a `configure()` method:

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
// config/WireBox.bx
class extends="coldbox.system.ioc.config.Binder" {

    function configure(){

    }

    function onLoad(){

    }

    function onShutdown(){

    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// config/WireBox.cfc
component extends="coldbox.system.ioc.config.Binder" {

    function configure(){

    }

    function onLoad(){

    }

    function onShutdown(){

    }
}
```
{% endtab %}
{% endtabs %}

**2. Simple configuration class** — create a class with a `configure( binder )` method that accepts a WireBox binder object:

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
// config/WireBox.bx
class {

    function configure( required binder ){

    }

    function onLoad(){

    }

    function onShutdown(){

    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// config/WireBox.cfc
component {

    function configure( required binder ){

    }

    function onLoad(){

    }

    function onShutdown(){

    }

}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The latter approach will be less verbose when talking to the mapping DSL the Binder object exposes. However, both are fully functional and matter of preference.
{% endhint %}

From the `configure()` method you will be able to interact with the Binder methods or creating implicit DSL structures in order to configure WireBox for operation and also to create object mappings. From the `onLoad()` method you can also use it for mappings with main distinction that the WireBox machinery is now online (logging, events, caching, etc). This is necessary for leveraging `mapDirectory()` calls.

{% hint style="info" %}
Please also note that the Binder itself has a reference to the current Injector it belongs to (`getInjector()`).
{% endhint %}

When you instantiate the WireBox injector, pass either the class path to your binder or an instance of it:

{% tabs %}
{% tab title="BoxLang" %}
```java
// Path-based
new coldbox.system.ioc.Injector( "path.to.my.Binder" )

// Instance-based
var oBinder = new path.to.my.Binder()
new coldbox.system.ioc.Injector( oBinder )
```
{% endtab %}
{% tab title="CFML" %}
```javascript
new wirebox.system.ioc.Injector( "path.to.my.Binder" );
// or
var oBinder = createObject( "path.to.my.Binder" );
new wirebox.system.ioc.Injector( oBinder );
```
{% endtab %}
{% endtabs %}

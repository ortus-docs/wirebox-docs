# Binder Configuration Properties

Whether you use WireBox standalone or within a ColdBox context, a Binder gets a structure of configuration properties so it can use them whenever you are configuring it or declaring mappings. If you are in **standalone** mode, the Injector can be constructed with a **properties** structure that will be passed to the binder for usage.&#x20;

{% hint style="info" %}
If you are in a ColdBox application, the ColdBox application configuration structure is passed to you.&#x20;
{% endhint %}

You can then use these properties with the following methods in your Binder:

* `getProperty( name, [default] )` : Get a specific property
* `getProperties()` : Get all the properties structure
* `propertyExists( name )` : Check if a property exists
* `setProperty( name, value )` : Dynamically add properties to the structure

```cfscript
// Init with your own properties
new wirebox.system.ioc.Injector( properties = myProps )
```

# WireBox Injector

<img src="../images/injector_DIUniverse.jpg">

WireBox bases itself on the idea of creating object injectors (`wirebox.system.ioc.Injector`) that in turn will produce and wire all your objects. You can create as many injector instances as you like in your applications, each with configurable differences or be linked hierarchically by setting each other as parent injectors. 

Each injector can be configured with a configuration binder or none at all. If you are a purely annotations based kind of developer and don't mind requesting pathed components by convention, then you can use the no-configuration approach and not even have a single configuration file, all using autowiring and discovery of conventions. However, if you would like to alter the behavior of the injector and also create object mappings, you will need a configuration binder. The next section explains the way to create this configuration binder, below is how to startup or bootstrap the injector in different manners:

**No Configuration Binder:**

```js
myObject = new coldbox.system.ioc.Injector().getInstance("my.object");
```

**With a Configuration Binder:**
```js
myObject = new coldbox.system.ioc.Injector("myBinderPath").getInstance("CoolObject");
```
The WireBox injector class is the pivotal class that orchestrates DI, instance events and so much more. We really encourage you to study its [API Docs](http://www.coldbox.org/api) to learn more about its construction and usage methods.





# Activate The AOP Listener

WireBox has an amazing event driven architecture that can help you modify, listen and do all kinds of magic during object creation, wiring, etc. Our AOP implementation is just a listener (`wirebox.system.aop.Mixer`) that will transform objects once they are finalized with dependency injection. This means, our AOP engine is completely decoupled from the internals of the DI engine and is incredibly fast and light weight. 

So let's activate it in our WireBox binder configuration:

```js
wirebox.listeners = [
	{ class="wirebox.system.aop.Mixer", properties={} }
];
```

That's it! That tells WireBox to register the AOP engine once it loads. This listener also has some properties that you can tweak:

| Property | Type | Required | Default | Description |
| -- | -- | -- | -- | -- |
| generationPath |	cf include path	| false | `/wirebox/system/aop/tmp` | The location where UDF stubs will be generated to. This can be to disk or memory. |
| classMatchReload | boolean	| false |	false	| A cool flag to allow you to reload the class matching dictionary for development purposes only. |
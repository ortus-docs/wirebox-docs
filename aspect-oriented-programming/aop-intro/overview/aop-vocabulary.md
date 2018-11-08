# AOP Vocabulary

* **Aspect**: A modularization of a concern that cuts across multiple objects.
* **Target Object** : The object that will be applied with Aspects across certain methods or join points.
* **Join Point** : A point of execution in a target object that will be applied a specific aspect to it. This is usually the execution of a method.
* **Advice** : An action taken at a particular join point. Usually, before, after or around it.
* **AOP Proxy** : An object or method representation for the original join point or method.

WireBox has an amazing [event driven architecture](../../../usage/wirebox-event-model/) that can help you modify, listen and do all kinds of magic during object creation, wiring, etc. Our AOP implementation is just a listener that will transform objects once they are finalized with dependency injection. This means, our AOP engine is completely decoupled from the interals of the DI engine and is incredibly fast and light weight. So let's activate it in our WireBox binder configuration:

```javascript
wirebox.listeners = [
    { class="coldbox.system.aop.Mixer",properties={} }
];
```

That's it! That tells WireBox to register the AOP engine once it loads. This listener also has some properties that you can tweak:

| Property | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| `generationPath` | cf include path | false | `/wirebox/system/aop/tmp` | The location where UDF stubs will be generated to. This can be to disk or memory. |
| `classMatchReload` | boolean | false | false | A cool flag to allow you to reload the class matching dictionary for development purposes only. |


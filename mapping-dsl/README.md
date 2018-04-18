# Mapping DSL

The mapping DSL is the way to configure object mappings in WireBox that will represent objects, factories or providers.  All mappings DSL methods return back an instance of the binder so you can concatenate methods to create readable execution chains.

The chains are divided into three types:

1. **Initiators** - Start the mapping DSL process
2. **Modifiers** - Can modify a mapping with metadata and behavior
3. **Destinations** - Tells the binder to what object or behavior we should map to.

{% hint style="danger" %}
If a mapping does not have a destination, then the information stored in the chain can bleed into other mappings.
{% endhint %}

```javascript
map( "Luis" )
    .to( "model.Likes.Espresso" )
    .asEagerInit()
    .asSingleton();
```


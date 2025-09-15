# Injection Idioms

Now that we have constructed our injector let's discuss a little about injection idioms or styles WireBox offers before we go all cowboy and start configuring and using this puppy. The styles shown below are written in execution order.

### Constructor (1)

**Motivation**: Mandatory dependencies for object creation

Each constructor argument receives a inject annotation with its required injection DSL. Be careful when dealing with object circular dependencies as they will fail via constructor injection due to its chicken and the egg nature

### Object Properties (2)

**Motivation**: Great documentable approach to variable mixins to reduce getter/setter verbosity

Leverages the greatest aspect of ColdFusion, **the dynamic language**, to mixin variables at runtime by using the `cfproperty` annotations. Great for documentation and visualizing object dependencies and **safe** for circular dependencies.&#x20;

Cons is that you **can not** use the dependencies in an object's **constructor** method-- instead use `onDIComplete()`.

### Setter Methods (3)

**Motivation**: Legacy classes

The inject annotation **MUST** exist on the setter method if the object is not mapped. Mapping must be done if you do not have access to the source or you do not want to touch the source.

Cons is that you **can not** use the dependencies in an object's **constructor** method-- instead use `onDIComplete()`.

## Summary

These are the three injection styles that WireBox supports and which style you choose depends on your requirements and also your personal taste. The **setter** method approach is linked to the way Spring and ColdSpring approach it which is the traditional JavaBean style of `setXXX` where `XXX` is the name of the mapping or object to pass into the setter method for injection.

{% hint style="info" %}
**Note** Whichever injection style you use with WireBox, the target's visibility does not matter. This means that you can create private or package methods and WireBox will still inject them for you. This is absolutely great when you are an encapsulation freak and you do not want to expose public setter methods.
{% endhint %}

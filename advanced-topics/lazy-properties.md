---
description: Wanna be lazy?
---

# Lazy Properties

WireBox supports the concept of marking properties in your components as `lazy`. This will allow the property to be constructed **ONCE** when requested _**ONLY** (lazy loaded)_. This way, you can take advantage of the construction of the property being lazy-loaded for you. &#x20;

{% hint style="warning" %}
Please note that this is different than providers since in this case, you provide the function that will build the property and it can be anything you want.
{% endhint %}

Internally, we will generate a _getter_ method for you that will make sure to construct your property via a builder function you will provide, lock the request (by default), store it in the `variables` scope, and return it to you.

> **Note**: With lazy properties, you must use the _getter_ only to retrieve the property ONLY!

```cfscript
component{
	
	// Lazy property: Constructed by convention via the buildUtil() method
	property name="util" lazy;

	/**
	 * Build a util object lazyily.
	 * The first time you call it, it will lock, build it, and store it by convention as 'variables.util'
	 */
	function buildUtil(){
		return new coldbox.system.core.util.Util();
	}

}
```

### Implicit Builder

When you tag a property as `lazy`, we will look for a method using the following pattern by convention:

```jsx
function build{propertyName}(){}
```

We will lock, call the builder, store the property and return it.

### Explicit Builder

If you want to use **ANY** method in your CFC to build the property, then use the value of the `lazy` annotation to point to the public or private method that will build your property:

```cfscript
component{
	
	property name="data" lazy="constructData";

	function constructData(){
		return dataservice.buildStrongData();
	}

}
```

### No Locking

By default, WireBox will lock the construction of the property. If you do not want the locking to occur, use the `LazyNoLock` attribute. Just as before, if you don’t have a value for the annotation, we will look for a `build{propertyName}` function, or if it has a value, we will use that as the name of the builder function.

```cfscript
component{
	
	property name="util" lazyNoLock;
	property name="util" lazyNoLock="constructUtil";

	/**
	 * Build a util object lazyily.
	 * The first time you call it, build it, and store it by convention as 'variables.util'
	 */
	function buildUtil(){
		return new coldbox.system.core.util.Util();
	}

	function constructUtil(){
		return new coldbox.system.core.util.Util();
	}

}
```

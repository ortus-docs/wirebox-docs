---
description: Observe any property and react!
---

# Property Observers

WireBox supports the concepts of component property observers. Meaning that you can define a function that will be called for you when the `setter` for that property has been called and thus observe the property changes within a component.

You will accomplish this by tagging a property with an annotation called `observed` and created a function called: `{propertyName}Observer` by convention. This function will receive three arguments:

* `newValue` : The value that will be set into the property
* `oldValue` : The old value of the property, including `null`
* `property` : The name of the property

```cfscript
component{

	property name="data" observed;

	/**
	 * Observer for data changes.  Anytime data is set, it will be called
   	 *
	 * @new The new value
	 * @old The old value
	 * @property The name of the property observed
	 */
	function dataObserver( newValue, oldValue, property ){
		// Execute after data is set
	}

}
```

If you don’t like the convention and want to name the function as you see fit, then you can place the value of the `observed` annotation as the name of the function to call.

```jsx

component{

	property name="data" observed="myObserver";

	/**
	 * Observer for data changes.  Anytime data is set, it will be called
  	 *
	 * @new The new value
	 * @old The old value
	 * @property The name of the property observed
	 */
	function myObserver( newValue, oldValue, property ){
		// Execute after data is set
	}

}
```

Please note that the observer will be called **AFTER** the property has been set.  That's it, enjoy!

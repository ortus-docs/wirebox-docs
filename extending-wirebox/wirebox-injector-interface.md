# WireBox Injector Interface

We also provide an interface to create objects that adhere to our injector interface: `wirebox.system.ioc.IInjector`.&#x20;

{% hint style="danger" %}
Please note that you DO NOT need to add the `implements` to your code.  We actually highly suggest you don't.  There are many issues with interfaces yet in multiple CFML engines.  So we do runtime checks for it, instead at compile time.
{% endhint %}

Then these objects can be used as parent injectors, which are great for legacy factories or creating hierarchies according to your specs. All you have to do is implement the following interface:

```javascript
/**
 * Copyright Since 2005 ColdBox Framework by Luis Majano and Ortus Solutions, Corp
 * www.ortussolutions.com
 * ---
 * An interface that enables any CFC to act like a parent injector within WireBox.
 **/
interface {

	/**
	 * Link a parent Injector with this injector and return itself
	 *
	 * @injector             A WireBox Injector to assign as a parent to this Injector
	 * @injector.doc_generic coldbox.system.ioc.Injector
	 *
	 * @return coldbox.system.ioc.IInjector
	 */
	function setParent( required injector );

	/**
	 * Get a reference to the parent injector instance, else an empty simple string meaning nothing is set
	 *
	 * @return coldbox.system.ioc.IInjector
	 */
	function getParent();

	/**
	 * Locates, Creates, Injects and Configures an object model instance
	 *
	 * @name          The mapping name or CFC instance path to try to build up
	 * @initArguments The constructor structure of arguments to passthrough when initializing the instance
	 * @dsl           The dsl string to use to retrieve the instance model object, mutually exclusive with 'name'
	 * @targetObject  The object requesting the dependency, usually only used by DSL lookups
	 * @injector      The child injector name to use when retrieving the instance
	 */
	function getInstance(
		name,
		struct initArguments = {},
		dsl,
		targetObject = "",
		injector
	);

	/**
	 * Checks if this injector can locate a model instance or not
	 *
	 * @name The object name or alias to search for if this container can locate it or has knowledge of it
	 */
	boolean function containsInstance( required name );

	/**
	 * Shutdown the injector gracefully by calling the shutdown events internally
	 *
	 * @return coldbox.system.ioc.IInjector
	 */
	function shutdown();

}

```

![](../.gitbook/assets/injectorInterface\_hierarchies.jpg)

Once you create this CFC that implements this interface then you can call on the injector's `setParent()` method and you are ready to roll.

```javascript
injector.setParent( myCustomInjector );
```

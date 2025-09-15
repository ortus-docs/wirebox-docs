# The Scope Interface

The scope interface can be found here: `coldbox.system.ioc.scopes.IScope`.&#x20;

{% hint style="danger" %}
Please note that you DO NOT need to add the `implements` to your code.  We actually highly suggest you don't.  There are many issues with interfaces yet in multiple CFML engines.  So we do runtime checks for it, instead at compile time.
{% endhint %}

```javascript
/**
 * Copyright Since 2005 ColdBox Framework by Luis Majano and Ortus Solutions, Corp
 * www.ortussolutions.com
 * ---
 * The main interface to produce WireBox storage scopes
 **/
interface {

	/**
	 * Configure the scope for operation and returns itself
	 *
	 * @injector             The linked WireBox injector
	 * @injector.doc_generic coldbox.system.ioc.Injector
	 *
	 * @return coldbox.system.ioc.scopes.IScope
	 */
	function init( required injector );

	/**
	 * Retrieve an object from scope or create it if not found in scope
	 *
	 * @mapping             The linked WireBox injector
	 * @mapping.doc_generic coldbox.system.ioc.config.Mapping
	 * @initArguments       The constructor struct of arguments to passthrough to initialization
	 */
	function getFromScope( required mapping, struct initArguments );


	/**
	 * Indicates whether an object exists in scope
	 *
	 * @mapping             The linked WireBox injector
	 * @mapping.doc_generic coldbox.system.ioc.config.Mapping
	 *
	 * @return coldbox.system.ioc.scopes.IScope
	 */
	boolean function exists( required mapping );

}

```

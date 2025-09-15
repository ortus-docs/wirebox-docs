# The DSL Builder Interface

### IDSLBuilder

The scope interface can be found here: `coldbox.system.ioc.dsl.IDSLBuilder`.&#x20;

{% hint style="danger" %}
Please note that you DO NOT need to add the `implements` to your code.  We actually highly suggest you don't.  There are many issues with interfaces yet in multiple CFML engines.  So we do runtime checks for it, instead at compile time.
{% endhint %}

```javascript
/**
 * Copyright Since 2005 ColdBox Framework by Luis Majano and Ortus Solutions, Corp
 * www.ortussolutions.com
 * ---
 * The main interface to produce WireBox namespace DSL Builders
 **/
interface {

	/**
	 * Configure the DSL Builder for operation and returns itself
	 *
	 * @injector             The linked WireBox Injector
	 * @injector.doc_generic coldbox.system.ioc.Injector
	 *
	 * @return coldbox.system.ioc.dsl.IDSLBuilder
	 */
	function init( required injector );

	/**
	 * Process an incoming DSL definition and produce an object with it
	 *
	 * @definition   The injection dsl definition structure to process. Keys: name, dsl
	 * @targetObject The target object we are building the DSL dependency for. If empty, means we are just requesting building
	 * @targetID     The target ID we are building this dependency for
	 *
	 * @return coldbox.system.ioc.dsl.IDSLBuilder
	 */
	function process( required definition, targetObject, targetID );

}

```

### Your DSL Builder

Here is a sample DSL builder:

```javascript
/**
 * Copyright Since 2005 ColdBox Framework by Luis Majano and Ortus Solutions, Corp
 * www.ortussolutions.com
 * ---
 * Process DSL functions via LogBox
 **/
component accessors="true" {

	/**
	 * Injector Reference
	 */
	property name="injector";

	/**
	 * LogBox Reference
	 */
	property name="logBox";

	/**
	 * Log Reference
	 */
	property name="log";

	/**
	 * Configure the DSL Builder for operation and returns itself
	 *
	 * @injector             The linked WireBox Injector
	 * @injector.doc_generic coldbox.system.ioc.Injector
	 *
	 * @return coldbox.system.ioc.dsl.IDSLBuilder
	 */
	function init( required injector ){
		variables.injector = arguments.injector;
		variables.logBox   = variables.injector.getLogBox();
		variables.log      = variables.injector.getLogBox().getLogger( this );

		return this;
	}

	/**
	 * Process an incoming DSL definition and produce an object with it
	 *
	 * @definition   The injection dsl definition structure to process. Keys: name, dsl
	 * @targetObject The target object we are building the DSL dependency for. If empty, means we are just requesting building
	 * @targetID     The target ID we are building this dependency for
	 *
	 * @return coldbox.system.ioc.dsl.IDSLBuilder
	 */
	function process( required definition, targetObject, targetID ){
		var thisType    = arguments.definition.dsl;
		var thisTypeLen = listLen( thisType, ":" );

		// DSL stages
		switch ( thisTypeLen ) {
			// logbox
			case 1: {
				return variables.logBox;
			}

			// logbox:root and logbox:logger
			case 2: {
				var thisLocationKey = getToken( thisType, 2, ":" );
				switch ( thisLocationKey ) {
					case "root": {
						return variables.logbox.getRootLogger();
					}
					case "logger": {
						return variables.logbox.getLogger( arguments.definition.name );
					}
				}
				break;
			}

			// Named Loggers
			case 3: {
				var thisLocationType = getToken( thisType, 2, ":" );
				var thisLocationKey  = getToken( thisType, 3, ":" );
				// DSL Level 2 Stage Types
				switch ( thisLocationType ) {
					// Get a named Logger
					case "logger": {
						// Check for {this} and targetobject exists
						if ( thisLocationKey eq "{this}" AND structKeyExists( arguments, "targetObject" ) ) {
							return variables.logBox.getLogger( arguments.targetObject );
						}
						// Normal Logger injection
						return variables.logBox.getLogger( thisLocationKey );
						break;
					}
				}
				break;
			}
			// end level 3 main DSL
		}
	}

}

```

Here is another one that you can find in the ColdBox ORM module: [https://github.com/coldbox-modules/cborm/tree/development/dsl](https://github.com/coldbox-modules/cborm/tree/development/dsl)

```javascript
/**
 * Copyright Since 2005 ColdBox Framework by Luis Majano and Ortus Solutions, Corp
 * www.ortussolutions.com
 * ---
 * The ORM WireBox DSL
 */
component accessors="true" {

	property name="injector";
	property name="log";


	/**
	 * Constructor as per interface
	 */
	public any function init( required any injector ){
		variables.injector = arguments.injector;
		variables.log      = arguments.injector.getLogBox().getLogger( this );

		return this;
	}

	/**
	 * Process an incoming DSL definition and produce an object with it
	 *
	 * @definition   The injection dsl definition structure to process. Keys: name, dsl
	 * @targetObject The target object we are building the DSL dependency for. If empty, means we are just requesting building
	 * @targetID     The target ID we are building this dependency for
	 *
	 * @return coldbox.system.ioc.dsl.IDSLBuilder
	 */
	function process( required definition, targetObject, targetID ){
		var DSLNamespace = listFirst( arguments.definition.dsl, ":" );

		switch ( DSLNamespace ) {
			case "entityService": {
				return getEntityServiceDSL( argumentCollection = arguments );
			}
		}
	}

	/**
	 * Get an EntityService Dependency
	 */
	function getEntityServiceDSL( required definition, targetObject ){
		var entityName = getToken( arguments.definition.dsl, 2, ":" );

		// Do we have an entity name? If we do create virtual entity service
		if ( len( entityName ) ) {
			return new cborm.models.VirtualEntityService( entityName );
		}

		// else return Base ORM Service
		return new cborm.models.BaseORMService();
	}

}

```

### Registration

In your configuration binder you can then register the DSL component you created

```javascript
customDSL = {
    ortus = "path.model.dsl.OrtusBuilder"
};

or
mapDSL("ortus","path.model.dsl.OrtusBuilder");
```

This will register a new injection DSL namespace called ortus that maps to that instantiation component `path.model.dsl.OrtusBuilder`.&#x20;

As you can see from the sample, creating your own DSL builder is fairly easy. The benefits of a custom DSL builder is that you can very easily create and extend the injection DSL language to your own benefit and if you are funky enough, override the behavior of the internal DSL Namespaces.

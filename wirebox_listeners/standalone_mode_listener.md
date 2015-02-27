# Standalone Mode Listener

<img src="../images/standaloneListener.jpg">

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Argument</b> </th>
<th><b>Type</b> </th>
<th><b>Execution Mode</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>interceptData</b> </td>
<td>struct </td>
<td><b>standalone-coldbox</b> </td>
<td>The data structure passed in the event </td></tr></tbody></table>

```javascript
component{

	function configure(injector,properties){
		variables.injector = arguments.injector;
		variables.properties = arguments.properties;

		log = variables.injector.getLogBox().getLogger( this );
	}

	function beforeInjectorShutdown(interceptData){
		// Do my stuff here:

		// I can use a log object because ColdBox is cool and injects one for me already.
		log.info("DUDE, I am going down!!!");
	}

	function afterInstanceCreation(interceptData){
		var target = arguments.interceptData.target;
		var mapping = arguments.interceptData.mapping;

		log.info("The object #mapping.getName()# has just been built, performing my awesome AOP processing on it.");

		// process awesome AOP on this target
		processAwesomeAOP( target );
	}
}
```
Please note the `configure()` method in the standalone listener. This is necessary when you are using Wirebox listeners outside of a ColdBox application. The `configure()` method receives two parameters:

* `injector` : An instance reference to the calling Injector where this listener will be registered with.
* `properties` : A structure of properties that passes through from the configuration file.

As you can see from the examples above, each Listener component can listen to multiple events. Now you might be asking yourself, in what order are these listeners executed in? Well, they are executed in the order they are declared in either the ColdBox configuration file as interceptors or the WireBox configuration file as listeners.

> **Important** Order is EXTREMELY important for interceptors/listeners. So please make sure you order them in the declaration file.


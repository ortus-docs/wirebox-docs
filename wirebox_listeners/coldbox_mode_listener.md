# ColdBox Mode Listener

<img src="../images/coldBoxListener.jpg">

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Argument</b> </th>
<th><b>Type</b> </th>
<th><b>Execution Mode</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>event</b> </td>
<td><i>coldbox.system.web.context.RequestContext</i> </td>
<td><b>coldbox</b> </td>
<td>The request context of the running request</td></tr>
<tr>
<td><b>interceptData</b> </td>
<td>struct </td>
<td><b>standalone-coldbox</b> </td>
<td>The data structure passed in the event </td></tr></tbody></table>

So let's say that we want to listen on the beforeInjectorShutdown and on the afterInstanceCreation event in our listener.

```javascript
component{

	function configure(){}

	function beforeInjectorShutdown(event, interceptData){
		var injector = arguments.interceptData.injector;
		// Do my stuff here:

		// I can use a log object because ColdBox is cool and injects one for me already.
		log.info("DUDE, I am going down!!!");
	}

	function afterInstanceCreation(event, interceptData){
		var injector = arguments.interceptData.injector;
		var target = arguments.interceptData.target;
		var mapping = arguments.interceptData.mapping;

		log.info("The object #mapping.getName()# has just been built, performing my awesome AOP processing on it.");

		// process awesome AOP on this target
		processAwesomeAOP( target );
	}
}
```

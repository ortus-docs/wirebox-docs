# Mapping Extra Attributes

You can store a-la-carte attributes in a specific mapping so it can be retrieved at a later time by either an AOP aspect or Events. This is a great way to store custom metadata about an object so it can be read later for some meaningful purpose. Let's say you want to tag a mapping with a custom type that is not so easily determined from the object instance itself. You don't want to do all kinds of introspection in order to know what object you received in an aspect or an event.

```javascript
map("MyHandler")
	.to("handlers.MyHandler")
	.extraAttributes({
		handlerPath = handlerLocation,
		module 		= arguments.module
	});
```

This mapping declares that an object has some extra attributes that will be stored in the mapping, such as the location and if it belongs to a module. This is then incredibly useful when you have an attached listener to WireBox:

```javascript
function afterInstanceAutowire(event, interceptData){
	var attribs = interceptData.mapping.getExtraAttributes();
	var iData 	= {};

	// listen to plugins only
	if( structKeyExists(attribs, "isPlugin") ){
		//Fill-up Intercepted MetaData
		iData.pluginPath = attribs.pluginPath;
		iData.custom 	 = attribs.custom;
		iData.module 	 = attribs.module;
		iData.oPlugin    = interceptData.target;

		//Fire My Own Custom Interception
		instance.interceptorService.processState("afterPluginCreation",iData);
	}
}
```

As you can see from this sample, the extra attributes are incredibly essential, as the listener just sends the target object. It would take lots of introspection and metadata inspections in order for me to determine if the incoming object is my system's plugin or not. However, with the extra attributes, it is just a snap!

# WireBox Events

WireBox's offers a wide gamut of life cycle events that are announced at certain points in execution time. Below are the current events announced by the Injector `wirebox.system.ioc.Injector`.

|Event|Data|Description|
|--|--|--|
|afterInjectorConfiguration|<ul><li><b>injector</b> : The calling injector reference </li></ul>|Called right after the injector has been fully configured for operation.|
|beforeInstanceCreation|<ul><li><b>mapping</b> : The mapping called to be created</li><li><b>injector</b> : The calling injector reference </li></ul>|Called right before an object mapping is built via our internal object builders or custom scope builders.|
|afterInstanceInitialized |<ul><li><b>mapping</b> : The mapping called to be created</li><li><b>target</b> : The object that just go constructed and initialized </li><li><b>injector</b> : The calling injector reference </li></ul>|Called after an object mapping gets constructed and initialized. The mapping has NOT been placed on a scope yet and no DI/AOP has been performed yet|
|afterInstanceCreation |<ul><li><b>mapping</b> : The mapping called to be created</li><li><b>target</b> : The object that just go built, initialized and DI/AOP performed on it </li><li><b>injector</b> : The calling injector reference </li></ul>|Called once the object has been fully created, initialized, stored, and DI/AOP performed on it. It is about to be returned to the caller via its <i>getInstance()</i> method.|
|beforeInstanceInspection |<ul><li><b>mapping</b> : The mapping that is about to be processed.</li><li><b>binder</b> : The configuration binder processing the mapping</li><li><b>injector</b> : The calling injector reference </li></ul>|Called whenever an object has been requested and its metadata has not been processed or discovered. In this interception point you can influence the metadata discovery.|
|afterInstanceInspection|<ul><li><b>mapping</b> : The mapping that is about to be processed.</li><li><b>binder</b> : The configuration binder processing the mapping</li><li><b>injector</b> : The calling injector reference </li></ul>|Called after an object mapping has been completely processed with its DI metadata discovery. This is your last chance to change or modify the DI data in the mapping before it is cached.|
|beforeInjectorShutdown |<ul><li><b>injector</b> : The calling injector reference </li></ul>|Called right before the Injector instance is shutdown.|
|afterInjectorShutdown |<ul><li><b>injector</b> : The calling injector reference </li></ul>|Called right after the Injector instance is shutdown.|
|beforeInstanceAutowire |<ul><li><b>injector</b> : The calling injector reference </li><li><b>mapping</b> : The instance mapping</li><li><b>target</b> : The target object for wiring</li><li><b>targetID</b> : The unique target object ID used for wiring</li></ul>|Called right after the instance has been created and initialized, but before DI wiring is done.|
|afterInstanceAutowire |<ul><li><b>injector</b> : The calling injector reference </li><li><b>mapping</b> : The instance mapping</li><li><b>target</b> : The target object for wiring</li><li><b>targetID</b> : The unique target object ID used for wiring </li></ul>|Called right after the instance has been created, initialized and DI has been completed on it.|


> **Note** Please see our [CacheBox](http://cachebox.ortusbooks.com) documentation to see all of CacheBox's events.

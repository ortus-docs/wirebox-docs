# Configuring WireBox

1. Create a simple configuration CFC that has a configure(binder) method that accepts a WireBox configuration binder object
```javascript
component{
	function configure(required binder){

	}
}
```
2. Create a configuration CFC that extends the WireBox configuration object: coldbox.system.ioc.config.Binder and has a configure() method.
```javascript
component extends="coldbox.system.ioc.config.Binder"{
	function configure(){

	}
}
```

<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="12%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
The latter approach will be less verbose when talking to the mapping DSL the Binder object exposes. However, both are fully functional and matter of preference.</b></p>
<div style="clear:both"></div>
</div>
<br>

From the configure() method you will be able to interact with the Binder methods or creating implicit DSL structures in order to configure WireBox for operation and also to create object mappings.

<br>
<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="12%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Please also note that the Binder itself has a reference to the current Injector it belongs to (getInjector()).</b></p>
<div style="clear:both"></div>
</div>
<br>






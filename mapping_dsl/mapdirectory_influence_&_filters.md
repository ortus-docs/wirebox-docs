# MapDirectory() Influence & Filters

The `mapDirectory()` allows you to leverage closures or UDF's to influence and filter mappings. The arguments are `filter` to add a filter that MUST return boolean in order to process the mapping and `influence` that can influence the created mapping with any custom bindings.

```js
// influence only certain components to be singleton
mapDirectory(packagePath="coldbox.testing.testModel.ioc", influence=function(binder, path){
	if( findNoCase( "simple", arguments.path) ){
		arguments.binder.asSingleton();
	}
});

// filter some components from registration
mapDirectory(packagePath="coldbox.testing.testModel.ioc", filter=function(path){
	return ( findNoCase( "simple", arguments.path ) ? false : true );
});
```

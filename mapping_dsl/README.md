# Mapping DSL
WireBox can also be configured by using the programmatic Mapping DSL exposed in the configuration binder instead of the implicit data structures DSL we just saw. Our recommendation is to use this mapping DSL as it makes your configuration become alive and more human readable than creating a bunch of arrays and structures. All mappings DSL methods return back an instance of the binder so you can concatenate methods to create readable execution chains:

```javascript
map("Lui")
	.to("model.Awesomeness")
	.asEagerInit()
	.asSingleton();

```




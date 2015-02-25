# Parent Object Definitions

Thanks to Phill Nacelli, you can reuse object definitions in your binder or via annotations. This means that you can declare an object with its dependencies and then create other definitions that use all of this parent object's definitions. This saves tons of time in declarations and provides you with great reusability.

```javascript
// Binder method
parent(alias);

// Parent Annotation
component parent="alias"{}
```
Here is a small example:

```javascript
// PARENT Mappings
map("AbstractService").to("model.AbstractService");
	.property(name:"someAlphaDAO", ref:"someAlphaDAO")
	.property(name:"someBravoDAO", ref:"someBravoDAO");

// Concrete service with parent and also some added dpendencies of its own
map("ConcreteService").to("#myPath#.parent.SomeConcreteService")
	.parent("AbstractService")
	.property(name:"someCharlieDAO", ref:"someCharlieDAO")
	.property(name:"someDeltaDAO", ref:"someDeltaDAO");;
```

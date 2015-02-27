# Aspect Registration

Now that we have built our aspect we need to register it with WireBox so it nows about it and all DI can be performed in it. Let's open our WireBox binder and use the following DSL method:

* `mapAspect(aspect,autoBinding=[true])`

```javascript
mapAspect("MethodLogger").to("model.aspects.MethodLogger");
```

This tells WireBox to register a new aspect called MethodLogger that points to the CFC model.aspects.MethodLogger that I have just built. WireBox will then mark that object as an aspect, create it once the injector loads and have it ready for building.


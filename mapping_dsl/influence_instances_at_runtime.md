# Influence Instances at Runtime

You can use our mapping DSL to register influence closures or functions on a per mapping basis.  This will allow a developer to influence the requested instance of any object/data element and decorate objects or even return different objects.

This is similar to object providers but instead of overriding the ENTIRE creation process of the object like a provider does, the user might want to simply influence the creation of a *normal*  mapping with some additional flair.

```
map( 'myObject' )
   .toPath( 'com.foo.bar' )
   .withInfluence( function( injector, object ) {
      object.customSettings( true );
      object.pizzazz = 'Oh, yes!';
      return object;
});
```
In this instance, the instance is already built and then passed into the closure for additional influence. Note, the object is returned from the closure. Make this optional, but if something IS returned, it will override the instance which will allow a developer to replace or decorate the instance as they see fit.


# Influence Instances at Runtime

You can use our mapping DSL to register influence closures or lambdas on a per mapping basis. This will allow a developer to influence the requested instance of any object/data element and decorate objects or even return different objects.

This is similar to object providers but instead of overriding the ENTIRE creation process of the object like a provider does, the user might want to simply influence the creation of a _normal_ mapping with some additional flair. This is accomplished via the `withInfluence` mapping DSL function. It receives a closure as an argument and the closure has the following signature:

```
/**
* Influence an instance of an object
* @injector The WireBox injector reference
* @object The object to influence
*/
function( injector, object ){}
```

Here is an example of adding some nice pizzazz to an object:

```
map( 'myObject' )
   .toPath( 'com.foo.bar' )
   .withInfluence( function( injector, object ) {
      object.customSettings( true );
      object.pizzazz = 'Oh, yes!';
      return object;
});
```

In this instance, the instance is already built and then passed into the closure for additional influence. Please note, that the object is returned from the closure. You can make this optional, but if something **IS** returned, it will override the instance which will allow a developer to replace or decorate the instance as they see fit.

# toProvider() closures

The mapping destination `toProvider()` can also take a closure that will be executed whenever that mapping is requested. This allows you to add your own custom provider construction code inline without creating a standalone provider object that implements our provider interface. By leveraging closures you can really get funky and more concise in your coding. This closure will have the following signature and it must return the instance requested:

```
/**
* Create an instance of an object
* @injector The WireBox injector reference
*
* @return Any instance object
*/
function( injector ){}
```

Here is an example of how to accomplish this:

```javascript
map("MyEspresso").toProvider( function( injector ){
    var espresso = new Espresso( sugar=2, cream = true );
    arguments.injector.autowire( espresso );
    return espresso;
} );
```

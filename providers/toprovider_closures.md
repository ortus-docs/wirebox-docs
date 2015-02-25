# toProvider() closures
The mapping destination toProvider() can also take a closure that will be executed whenever that mapping is requested. This allows you to add your own custom provider construction code inline without creating a standalone provider object that implements our provider interface. By leveraging closures you can really get funky and more concise in your coding:

```javascript
map("MyEspresso").toProvider( function(){
	var espresso = new Espresso( sugar=2, cream = true );
	injector.autowire( espresso );
	return espresso;
} );
```

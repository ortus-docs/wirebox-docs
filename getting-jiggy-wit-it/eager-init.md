# Eager Init

Another aspect of our objects is when are they created? Good question! 

By default all objects are created **ONLY** when they are requested, in other words they are **lazy** created. But what if you are spoiled and you want your stuff NOW NOW NOW! Well, you can, cry if you want to! Just tell WireBox that you want your objects to be eagerly created. How? Via the mapping DSL and our cool `asEagerInit()` function.

```javascript
component extends = "wirebox.system.ioc.config.Binder" {

    function configure(){

        // map with shorthand or full scope notation
        mapPath("model.Coffeshop")
            .asSingleton()
            .asEagerInit();
    }
```


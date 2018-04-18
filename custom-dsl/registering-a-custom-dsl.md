# Registering a Custom DSL

```javascript
customDSL = {
    ortus = "path.model.dsl.MyDSL"
};

or
mapDSL("ortus","path.model.dsl.MyDSL");
```

Now I can use the `ortus` DSL Namespace in my mappings DSL and even my annotations, isn't that cool!

```javascript
// inject it
property name="funky" inject="ortus:funkyObject";

// map it
map("Luis")
    .toDSL("ortus:funkyObject");
```

## Dynamic Custom DSL Registration

Injectors allow you to register custom DSLs at runtime by using the `registerDSL()` method on any injector.

```javascript
// Register Custom DSL
controller.getWireBox()
    .registerDSL( namespace="javaloader", path="app.model.JavaLoaderDSL" );
```


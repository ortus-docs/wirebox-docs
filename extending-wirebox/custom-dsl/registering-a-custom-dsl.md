# Registering a Custom DSL

To register a custom namespace in WireBox, place the following configuration in the `wirebox` struct defined within the `configure()` method of your WireBox binder CFC. in a ColdBox app, this is `/config/WireBox.cfc`. Alternatively, you can use the `mapDSL()` call in the `configure()` method.

{% code-tabs %}
{% code-tabs-item title="/config/WireBox.cfc" %}
```javascript
component extends="coldbox.system.ioc.config.Binder" {

    function configure(){
        wirebox = {
            // DSL Namespace registrations
            customDSL = {
                ortus = "path.model.dsl.MyDSL"
            }
        };

        // Or here...        
        mapDSL("ortus","path.model.dsl.MyDSL");        
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you want to register a custom DSL namespace from a module, you can make the same call via the `binder` reference that is provided to your `ModuleConfig.cfc`.

{% code-tabs %}
{% code-tabs-item title="ModuleConfig.cfc" %}
```javascript
component {
    function configure() {
        binder.mapDSL("ortus","path.model.dsl.MyDSL");
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now I can use the `ortus` DSL Namespace in my mappings DSL and even my annotations, isn't that cool!

```javascript
// inject it into a CFC
property name="funky" inject="ortus:funkyObject";

// map it in your WireBox Binder
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


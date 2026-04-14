# Common Methods

The following chart shows you the most common methods when dealing with the WireBox Injector. This doesn't mean there are no other methods on the Injector that are of value, so please check out the CFC Docs for more in-depth knowledge.

{% embed url="https://s3.amazonaws.com/apidocs.ortussolutions.com/wirebox/current/index.html" %}
CFC Docs
{% endembed %}

{% tabs %}
{% tab title="BoxLang" %}
```java
// Send an object to WireBox for autowiring by convention or mapping lookups
autowire( target, [mapping], [targetID], [annotationCheck] )

// Clears all singleton instances from the singleton scope (handy in development)
clearSingletons()

// Checks if this injector can build the named instance
containsInstance( name )

// Get the configuration binder for this injector
getBinder()

// The primary method to request an object instance by name, DSL string, or child injector
getInstance( [name], [initArguments], [dsl], [targetObject], [injector] )

// Return the WireBox ObjectPopulator utility (populate objects from JSON, XML, structs, etc.)
getObjectPopulator()

// Get a reference to the parent injector (if any)
getParent()

// Get a reference to a registered persistence scope by name
getScope( name )

// Set or replace the parent injector
setParent( injector )

// Gracefully shut down the injector and all child injectors
shutdown()

// Return the injector's unique name (e.g. 'root')
getName()

// -----------------------------------------------
// Child Injector Methods
// -----------------------------------------------

// Check whether a named child injector has been registered
hasChildInjector( name )

// Register a child injector, setting this injector as its parent
registerChildInjector( name, child )

// Remove and shut down a child injector by name
removeChildInjector( name )

// Get a registered child injector by name
getChildInjector( name )

// Return an array of all registered child injector names
getChildInjectorNames()
```
{% endtab %}
{% tab title="CFML" %}
```javascript
// A method you can use to send objects to get autowired by convention or mapping lookups
autowire(target,[mapping],[targetID],[annotationCheck])

// A utility method that clears all the singletons from the singleton persistence scope. Great to do in development.
clearSingletons()

// Checks if an instance can be created by this Injector or not
containsInstance(name)

// Get the configuration binder for this injector
getBinder()

// The main method that asks the injector for an object instance by name or by autowire DSL string.
// 'injector' routes the request to a named child injector
getInstance([name],[initArguments],[dsl],[targetObject],[injector])

// Retrieve the ColdBox object populator that can populate objects from JSON, XML, structures and much more.
getObjectPopulator()

// Get a reference to the parent injector (if any)
getParent()

// Get a reference to a registered persistence scope
getScope(name)

// Set a parent injector into the target injector to create hierarchies
setParent(injector)

// Gracefully shut down the injector and all child injectors
shutdown()

// Return the injector's registered name
getName()

// -----------------------------------------------
// Child Injector Methods
// -----------------------------------------------

// Check whether a named child injector has been registered
hasChildInjector(name)

// Register a child injector by name, making this its parent
registerChildInjector(name, child)

// Remove and shut down a child injector by name
removeChildInjector(name)

// Get a registered child injector by name
getChildInjector(name)

// Return an array of all registered child injector names
getChildInjectorNames()
```
{% endtab %}
{% endtabs %}

## `getInstance()` – `injector` Argument

The `injector` argument lets you route a creation request directly to a registered child injector:

{% tabs %}
{% tab title="BoxLang" %}
```java
// Create 'MyService' using the child injector named 'plugins'
var svc = wirebox.getInstance( name : "MyService", injector : "plugins" )
```
{% endtab %}
{% tab title="CFML" %}
```javascript
// Create 'MyService' using the child injector named 'plugins'
var svc = wirebox.getInstance( name="MyService", injector="plugins" );
```
{% endtab %}
{% endtabs %}

## Child Injectors

Child injectors allow you to create isolated DI scopes nested within a parent injector. A child inherits parent lookups but its own mappings are isolated.

{% tabs %}
{% tab title="BoxLang" %}
```java
// Bootstrap a child injector with its own binder
var child = new coldbox.system.ioc.Injector( "plugins.PluginsBinder" )

// Register it under the parent
wirebox.registerChildInjector( "plugins", child )

// Later: retrieve from child
var plugin = wirebox.getInstance( name : "MyPlugin", injector : "plugins" )

// Remove the child injector when no longer needed
wirebox.removeChildInjector( "plugins" )
```
{% endtab %}
{% tab title="CFML" %}
```javascript
// Bootstrap a child injector with its own binder
var child = new coldbox.system.ioc.Injector( "plugins.PluginsBinder" );

// Register it under the parent
wirebox.registerChildInjector( "plugins", child );

// Later: retrieve from child
var plugin = wirebox.getInstance( name="MyPlugin", injector="plugins" );

// Remove the child injector when no longer needed
wirebox.removeChildInjector( "plugins" );
```
{% endtab %}
{% endtabs %}

# Common Methods

The following chart shows you the most common methods when dealing with the WireBox Injector. This doesn't mean there are no other methods on the Injector that are of value, so please check out the CFC Docs for more in-depth knowledge.

```javascript
// A method you can use to send objects to get autowired by convention or mapping lookups
autowire(target,[mapping],[targetID],[annotationCheck]) </td>

// A utility method that clears all the singletons from the singleton persistence scope. Great to do in development.
clearSingletons()

// Checks if an instance can be created by this Injector or not
containsInstance(name)

// Get the configuration binder for this injector
getBinder()

// The main method that asks the injector for an object instance by name or by autowire DSL string.
getInstance([name],[initArguments],[dsl],[targetObject])

// Retrieve the ColdBox object populator that can populate objects from JSON, XML, structures and much more.
getObjectPopulator()

// Get a reference to the parent injector (if any)
getParent()

// Get a reference to a registered persistence scope
getScope(name)

// Set a parent injector into the target injector to create hierarchies
setParent(injector)
```


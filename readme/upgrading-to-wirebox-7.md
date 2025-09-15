---
description: The official WireBox 7 upgrade guide
---

# Upgrading to WireBox 7

### ColdFusion 2016 Support Dropped <a href="#coldfusion-2016-support-dropped" id="coldfusion-2016-support-dropped"></a>

ColdFusion 2016 support has been dropped. Adobe doesn't support them anymore, so neither do we.

### Testing Injector Creations

If you are creating your own WireBox injector in your tests and using integration testing, you will have Injector collisions.

```javascript
myInjector = new coldbox.system.ioc.Injector()
```

This affects **EVERY** version of WireBox because the default behavior of instantiating an Injector like the code above is to put the Injector in application scope: `application.wirebox.` This means that the REAL injector in an integration test lives in `application.wirebox` will be overridden.  To avoid this collision, disable scope registration:

```javascript
myInjector = new coldbox.system.ioc.Injector( {
    scopeRegistration : { enabled : false }hj
} )
```

## Custom Wirebox DSLs

For those of you with custom wirebox DSLs, you'll need to update your DSL to match the new `process()` method signature:

```js

/**
 * Process an incoming DSL definition and produce an object with it
 *
 * @definition   The injection dsl definition structure to process. Keys: name, dsl
 * @targetObject The target object we are building the DSL dependency for. If empty, means we are just requesting building
 * @targetID     The target ID we are building this dependency for
 *
 * @return coldbox.system.ioc.dsl.IDSLBuilder
 */
function process( required definition, targetObject, targetID );
```

### BeanPopulator Deprecated

The object `BeanPopulator` has been deprecated in favor of `ObjectPopulator`.

---
description: The official WireBox 8 upgrade guide
---

# Upgrading to WireBox 8

An upgrade from WireBox 7 should not incur any breaking changes, but you should still read through the guide to ensure you are not using any deprecated or removed features.

## ColdFusion 2018-2021 Support Dropped

ColdFusion 2018-2021 support has been dropped. Adobe doesn't support them anymore, so neither do we.

## Removals

### BeanPopulator

The `BeanPopulator` class has been removed.  This class was deprecated in ColdBox 6 and was replaced by the `ObjectPopulator` class.  Please use `coldbox.system.core.dynamic.ObjectPopulator` instead.

### ColdBox Util Env/System Methods

The following methods were removed in preference to the Environment Delegate class: `coldbox.system.core.delegates.Env`.

```js
/**
* @deprecated Refactor to use the Env Delegate: coldbox.system.core.delegates.Env
*/
function getSystemSetting( required key, defaultValue ){
    return new coldbox.system.core.delegates.Env().getSystemSetting( argumentCollection = arguments );
}

/**
* @deprecated Refactor to use the Env Delegate: coldbox.system.core.delegates.Env
*/
function getSystemProperty( required key, defaultValue ){
    return new coldbox.system.core.delegates.Env().getSystemProperty( argumentCollection = arguments );
}

/**
* @deprecated Refactor to use the Env Delegate: coldbox.system.core.delegates.Env
*/
function getEnv( required key, defaultValue ){
    return new coldbox.system.core.delegates.Env().getEnv( argumentCollection = arguments );
}
```

### Binder.getProperty() `default` Argument Removed

The `default` argument was deprecated in ColdBox 6 and has now been removed.  Please use `defaultValue` instead.

### Binder.getCacheBoxConfig() Removed

The `getCacheBoxConfig()` method was deprecated in ColdBox 6 and has now been removed.  Please use `getCacheBox()` instead.

### InterceptorService.processState() Removed

The `processState()` method has been removed from the `InterceptorService` ([COLDBOX-1358](https://ortussolutions.atlassian.net/browse/COLDBOX-1358)). This method was deprecated and has now been completely removed.

**Migration:** Use the `announce()` method instead.

```js
// Old way - removed
interceptorService.processState( "myEvent", data );

// New way - use announce()
interceptorService.announce( "myEvent", data );
```

## Deprecations

The following methods were deprecated in WireBox 7 and will be removed in WireBox 9.

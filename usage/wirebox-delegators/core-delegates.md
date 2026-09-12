---
description: Built-in delegates shipped with ColdBox/WireBox for common everyday tasks
---

# Core Delegates

WireBox ships with a set of built-in **core delegates** that you can drop into any object in your application. They are registered under the `@coreDelegates` WireBox namespace, so you only need to reference them by their short name.

{% hint style="success" %}
Core delegates work in both **BoxLang** and **CFML** and can be composed using the `delegates` class annotation or individual `property` injections.
{% endhint %}

## Available Core Delegates

| WireBox ID                   | Class Path                                      | Description                                             |
| ---------------------------- | ----------------------------------------------- | ------------------------------------------------------- |
| `Async@coreDelegates`        | `coldbox.system.core.delegates.Async`           | Async/parallel programming via the ColdBox AsyncManager |
| `DateTime@coreDelegates`     | `coldbox.system.core.delegates.DateTime`        | Date and time utilities via DateTimeHelper              |
| `Env@coreDelegates`          | `coldbox.system.core.delegates.Env`             | Java system properties and OS environment variables     |
| `Flow@coreDelegates`         | `coldbox.system.core.delegates.Flow`            | Fluent flow-control methods for expressive chaining     |
| `JsonUtil@coreDelegates`     | `coldbox.system.core.delegates.JsonUtil`        | JSON serialization utilities                            |
| `Population@coreDelegates`   | `coldbox.system.core.delegates.Population`      | Object population from structs, JSON, XML, and queries  |
| `StringUtil@coreDelegates`   | `coldbox.system.core.delegates.StringUtil`      | String manipulation and formatting utilities            |

## How to Use Core Delegates

Use the `delegates` class annotation for a concise declaration:

{% tabs %}
{% tab title="BoxLang" %}
```java
// Single delegate
class delegates="Flow@coreDelegates" {
}

// Multiple delegates
class delegates="Flow@coreDelegates, StringUtil@coreDelegates, Env@coreDelegates" {
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// Single delegate
component delegates="Flow@coreDelegates" {
}

// Multiple delegates
component delegates="Flow@coreDelegates, StringUtil@coreDelegates, Env@coreDelegates" {
}
```
{% endtab %}
{% endtabs %}

Or use individual `property` injections when you need prefixes/suffixes or targeted method lists:

{% tabs %}
{% tab title="BoxLang" %}
```java
class {

    property name="flow"       inject="Flow@coreDelegates"       delegate;
    property name="stringUtil" inject="StringUtil@coreDelegates" delegate;
    property name="population" inject="Population@coreDelegates" delegate;

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component {

    property name="flow"       inject="Flow@coreDelegates"       delegate;
    property name="stringUtil" inject="StringUtil@coreDelegates" delegate;
    property name="population" inject="Population@coreDelegates" delegate;

}
```
{% endtab %}
{% endtabs %}

---

## Async

**WireBox ID:** `Async@coreDelegates`\
**Class:** `coldbox.system.core.delegates.Async`

Provides access to the ColdBox `AsyncManager` and its most common utilities for asynchronous and parallel programming.

### Methods

| Method              | Description                                                                 |
| ------------------- | --------------------------------------------------------------------------- |
| `async()`           | Returns the `AsyncManager` instance directly                                |
| `newFuture(...)`    | Delegated from `AsyncManager` — creates and returns a new `Future` object   |
| `arrayRange(...)`   | Delegated from `AsyncManager` — creates a ranged parallel stream from an array |

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="Async@coreDelegates" {

    function process() {
        // Get the AsyncManager directly
        var manager = async()

        // Use delegated methods
        var result = newFuture( () => expensiveOperation() )
            .get()

        // Parallel array work
        arrayRange( [1,2,3,4,5], ( item ) => processItem( item ) )
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="Async@coreDelegates" {

    function process() {
        // Get the AsyncManager directly
        var manager = async()

        // Use delegated methods
        var result = newFuture( function() { return expensiveOperation() } )
            .get()

        // Parallel array work
        arrayRange( [1,2,3,4,5], function( item ) { return processItem( item ) } )
    }

}
```
{% endtab %}
{% endtabs %}

---

## DateTime

**WireBox ID:** `DateTime@coreDelegates`\
**Class:** `coldbox.system.core.delegates.DateTime`

Delegates **all** public methods from `coldbox.system.async.time.DateTimeHelper` directly onto your class, giving you a rich date/time API without any extra boilerplate.

{% hint style="info" %}
Since all methods come from `DateTimeHelper`, refer to its [API docs](https://s3.amazonaws.com/apidocs.ortussolutions.com/coldbox/current/coldbox/system/async/time/DateTimeHelper.html) for the full method list.
{% endhint %}

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="DateTime@coreDelegates" {

    function getNextWeek() {
        return now().plusDays( 7 )
    }

    function isExpired( required date expiresAt ) {
        return expiresAt.isBefore( now() )
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="DateTime@coreDelegates" {

    function getNextWeek() {
        return now().plusDays( 7 )
    }

    function isExpired( required date expiresAt ) {
        return expiresAt.isBefore( now() )
    }

}
```
{% endtab %}
{% endtabs %}

---

## Env

**WireBox ID:** `Env@coreDelegates`\
**Class:** `coldbox.system.core.delegates.Env`

Provides utilities for reading Java system properties and OS environment variables. Methods search Java system properties first, then environment variables unless specified otherwise.

### Methods

| Method                                      | Description                                                                                                   |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `getSystemSetting( key, defaultValue )`     | Returns the value from **Java system properties first, then OS env vars**. Throws `SystemSettingNotFound` if missing and no default given. |
| `getSystemProperty( key, defaultValue )`    | Returns a **Java system property** (`-Dkey=value`) only. Throws `SystemSettingNotFound` if missing and no default given. |
| `getEnv( key, defaultValue )`               | Returns an **OS environment variable** only. Throws `SystemSettingNotFound` if missing and no default given.  |
| `getJavaSystem()`                           | Returns the raw `java.lang.System` instance.                                                                  |

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="Env@coreDelegates" {

    function getDatabaseUrl() {
        // Checks system properties first, then env vars, with a fallback default
        return getSystemSetting( "DB_URL", "jdbc:h2:mem:testdb" )
    }

    function getPort() {
        // Env var only, required — throws if missing
        return getEnv( "SERVER_PORT" )
    }

    function getAppMode() {
        return getSystemProperty( "app.mode", "production" )
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="Env@coreDelegates" {

    function getDatabaseUrl() {
        // Checks system properties first, then env vars, with a fallback default
        return getSystemSetting( "DB_URL", "jdbc:h2:mem:testdb" )
    }

    function getPort() {
        // Env var only, required — throws if missing
        return getEnv( "SERVER_PORT" )
    }

    function getAppMode() {
        return getSystemProperty( "app.mode", "production" )
    }

}
```
{% endtab %}
{% endtabs %}

---

## Flow

**WireBox ID:** `Flow@coreDelegates`\
**Class:** `coldbox.system.core.delegates.Flow`

Provides fluent flow-control methods modeled after functional programming patterns. All methods return the parent object so you can chain calls expressively.

{% hint style="warning" %}
`Flow` is a **transient** delegate. If you inject it into a **singleton**, WireBox will correctly handle the `$parent` reference per-injection, but be aware that shared state issues can arise. Prefer using the class `delegates` annotation so WireBox manages the lifecycle.
{% endhint %}

### Methods

| Method                                        | Description                                                                                   |
| --------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `peek( target )`                              | Executes the closure with the parent as its argument and returns the parent for chaining.     |
| `when( target, success, failure )`            | Runs `success` if `target` is truthy; runs `failure` if provided and target is falsy.        |
| `unless( target, success, failure )`          | Runs `success` if `target` is falsy; runs `failure` if provided and target is truthy.        |
| `throwIf( target, type, message, detail )`    | Throws an exception if `target` evaluates to `true`.                                         |
| `throwUnless( target, type, message, detail )`| Throws an exception if `target` evaluates to `false`.                                        |
| `ifNull( target, success, failure )`          | Runs `success` if `target` is `null`; runs `failure` if provided and target is not null.     |
| `ifPresent( target, success, failure )`       | Runs `success` if `target` is **not** `null`; runs `failure` if provided and target is null. |

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="Flow@coreDelegates" {

    function save( required struct data ) {
        return this
            .throwIf( data.isEmpty(), "ValidationException", "Data cannot be empty" )
            .when( data.keyExists( "email" ), () => validateEmail( data.email ) )
            .peek( (self) => logBox.getRootLogger().info( "Saving #data.name#" ) )
    }

}

// Fluent chaining on any WireBox object with the Flow delegate
user
    .setName( "Luis" )
    .setAge( 21 )
    .peek( (u) => println( u.getName() ) )
    .when( user.isAdmin(), () => user.setRole( "admin" ) )
    .throwUnless( user.isValid(), "InvalidUser", "User is not valid" )
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="Flow@coreDelegates" {

    function save( required struct data ) {
        return this
            .throwIf( data.isEmpty(), "ValidationException", "Data cannot be empty" )
            .when( data.keyExists( "email" ), function() { validateEmail( data.email ) } )
            .peek( function( self ) { logBox.getRootLogger().info( "Saving #data.name#" ) } )
    }

}

// Fluent chaining on any WireBox object with the Flow delegate
user
    .setName( "Luis" )
    .setAge( 21 )
    .peek( function( u ) { writeDump( u.getName() ) } )
    .when( user.isAdmin(), function() { user.setRole( "admin" ) } )
    .throwUnless( user.isValid(), "InvalidUser", "User is not valid" )
```
{% endtab %}
{% endtabs %}

---

## JsonUtil

**WireBox ID:** `JsonUtil@coreDelegates`\
**Class:** `coldbox.system.core.delegates.JsonUtil`

Provides opinionated JSON serialization utilities. The `toJson`, `prettyJson`, and `toPrettyJson` methods are delegated from `coldbox.system.core.util.Util`.

### Methods

| Method                   | Description                                                                                          |
| ------------------------ | ---------------------------------------------------------------------------------------------------- |
| `toJson( data )`         | Serializes any data to a JSON string.                                                                |
| `prettyJson( data )`     | Serializes data to an indented, human-readable JSON string.                                          |
| `toPrettyJson( data )`   | Alias for `prettyJson()`.                                                                            |
| `forAttribute( data )`   | Serializes to JSON (or leaves as-is if simple value) then encodes the result for safe HTML attribute use. |

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="JsonUtil@coreDelegates" {

    function toApiResponse( required struct data ) {
        return {
            raw       : toJson( data ),
            pretty    : prettyJson( data ),
            attribute : forAttribute( data )
        }
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="JsonUtil@coreDelegates" {

    function toApiResponse( required struct data ) {
        return {
            raw       : toJson( data ),
            pretty    : prettyJson( data ),
            attribute : forAttribute( data )
        }
    }

}
```
{% endtab %}
{% endtabs %}

---

## Population

**WireBox ID:** `Population@coreDelegates`\
**Class:** `coldbox.system.core.delegates.Population`

Provides object population backed by the WireBox Object Populator. Delegates can be used to bind incoming data from forms, REST APIs, XML feeds, or database queries directly onto your object properties.

{% hint style="info" %}
The `target` argument defaults to `$parent`, meaning the delegate will populate **itself** (the object that declared the delegation). You can override `target` to populate a different object.
{% endhint %}

### Methods

| Method                                    | Description                                                                           |
| ----------------------------------------- | ------------------------------------------------------------------------------------- |
| `populate( memento, ... )`                | Populate from a struct/map.                                                           |
| `populateWithPrefix( memento, prefix, ... )` | Populate using prefixed keys (e.g., `user_name` → `name` with prefix `user`).     |
| `populateFromJSON( JSONString, ... )`     | Populate from a JSON string.                                                          |
| `populateFromXML( xml, root, ... )`       | Populate from an XML string or XML object.                                            |
| `populateFromQuery( qry, rowNumber, ... )`| Populate from a query row.                                                            |

All methods accept the following common arguments:

| Argument                 | Default | Description                                                              |
| ------------------------ | ------- | ------------------------------------------------------------------------ |
| `scope`                  | `""`    | Use scope injection instead of setters                                   |
| `trustedSetter`          | `false` | Call setters without checking if they exist (useful with `onMissingMethod`) |
| `include`                | `""`    | Comma-delimited list of keys to populate exclusively                     |
| `exclude`                | `""`    | Comma-delimited list of keys to skip                                     |
| `ignoreEmpty`            | `false` | Skip empty values during population                                      |
| `nullEmptyInclude`       | `""`    | Keys to set to `null` when the incoming value is empty                   |
| `nullEmptyExclude`       | `""`    | Keys to **not** set to `null` when empty                                 |
| `composeRelationships`   | `false` | Automatically compose object relationships from the incoming data        |
| `ignoreTargetLists`      | `false` | Ignore population include/exclude metadata defined on the target itself  |

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="Population@coreDelegates" {

    function update( required struct data ) {
        // Populates this object (via $parent) — ignores empty values
        return populate( memento: data, ignoreEmpty: true )
    }

    function updateFromForm( required struct formData ) {
        // All form fields are prefixed with "user_"
        return populateWithPrefix(
            memento : formData,
            prefix  : "user",
            exclude : "password"
        )
    }

    function updateFromJson( required string json ) {
        return populateFromJSON( JSONString: json, trustedSetter: true )
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="Population@coreDelegates" {

    function update( required struct data ) {
        // Populates this object (via $parent) — ignores empty values
        return populate( memento: data, ignoreEmpty: true )
    }

    function updateFromForm( required struct formData ) {
        // All form fields are prefixed with "user_"
        return populateWithPrefix(
            memento : formData,
            prefix  : "user",
            exclude : "password"
        )
    }

    function updateFromJson( required string json ) {
        return populateFromJSON( JSONString: json, trustedSetter: true )
    }

}
```
{% endtab %}
{% endtabs %}

---

## StringUtil

**WireBox ID:** `StringUtil@coreDelegates`\
**Class:** `coldbox.system.core.delegates.StringUtil`

Provides string manipulation and formatting utilities covering case conversion, slugification, SQL formatting, and basic English pluralization.

### Methods

| Method                             | Description                                                                          |
| ---------------------------------- | ------------------------------------------------------------------------------------ |
| `prettySql( target )`              | Formats a SQL string with newlines and indentation for readability.                  |
| `slugify( str, maxLength, allow )` | Creates a URL-safe slug. `maxLength=0` means no limit; `allow` is a regex safe-list of extra allowed chars. |
| `camelCase( target )`              | Converts `snake_case` or `kebab-case` to `camelCase`.                                |
| `headline( target )`               | Converts a delimited or cased string to `Title Case With Spaces`.                   |
| `ucFirst( target )`                | Uppercases the first character of a string.                                          |
| `lcFirst( target )`                | Lowercases the first character of a string.                                          |
| `kebabCase( target )`              | Converts a string to `kebab-case`.                                                   |
| `snakeCase( target, delimiter )`   | Converts a string to `snake_case`. `delimiter` defaults to `_`.                     |
| `pluralize( word )`                | Returns the plural form of an English word.                                          |
| `singularize( word )`              | Returns the singular form of an English word.                                        |

### Usage

{% tabs %}
{% tab title="BoxLang" %}
```java
class delegates="StringUtil@coreDelegates" {

    function getPageSlug( required string title ) {
        return slugify( title, 100 )
        // "My Cool Post!" => "my-cool-post"
    }

    function getHeadline( required string raw ) {
        return headline( raw )
        // "myServiceName" => "My Service Name"
    }

    function getTableName( required string modelName ) {
        return pluralize( snakeCase( modelName ) )
        // "UserProfile" => "user_profiles"
    }

    function formatQuery( required string sql ) {
        return prettySql( sql )
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component delegates="StringUtil@coreDelegates" {

    function getPageSlug( required string title ) {
        return slugify( title, 100 )
        // "My Cool Post!" => "my-cool-post"
    }

    function getHeadline( required string raw ) {
        return headline( raw )
        // "myServiceName" => "My Service Name"
    }

    function getTableName( required string modelName ) {
        return pluralize( snakeCase( modelName ) )
        // "UserProfile" => "user_profiles"
    }

    function formatQuery( required string sql ) {
        return prettySql( sql )
    }

}
```
{% endtab %}
{% endtabs %}

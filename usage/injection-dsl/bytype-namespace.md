# ByType Namespace

The `bytype` namespace resolves a dependency by the **native type** declared on the property or constructor/setter argument, instead of by name. WireBox reads the type off the property/argument declaration itself and asks the injector to build/locate a mapping whose name matches that type - so the type you declare doubles as the lookup key.

This is handy when you want the argument/property name to be whatever reads best in your code, while the actual dependency to inject is driven purely by its class name/mapping alias.

### 1st Level DSL

| DSL      | Description                                                                                                              |
| -------- | -------------------------------------------------------------------------------------------------------------------------- |
| `bytype` | Look up and inject a mapped instance using the property, constructor argument, or setter's declared `type` as the mapping name. |

{% hint style="info" %}
The `type` isn't part of the `inject` value itself - it's the normal `type` attribute/type declaration you already put on the property or argument. WireBox simply reads it when `inject="bytype"` is used, and if no instance can be found matching that type it falls through like any other unresolved dependency (throwing unless `required=false`).
{% endhint %}

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
// Property injection: WireBox will look up a mapping named "UserService"
property name="userService" type="UserService" inject="bytype";

// Constructor injection: annotate the argument with @inject bytype and give it a real type
class {

    /**
     * @userService.inject bytype
     */
    function init( required UserService userService ){
        variables.userService = arguments.userService
        return this
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// Property injection: WireBox will look up a mapping named "UserService"
property name="userService" type="UserService" inject="bytype";

// Constructor injection: annotate the argument with @inject bytype and give it a real type
component {

    /**
     * @userService.inject bytype
     */
    function init( required UserService userService ){
        variables.userService = arguments.userService;
        return this;
    }

}
```
{% endtab %}
{% endtabs %}

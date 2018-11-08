# ID-Model-Empty Namespace

The default namespace is not specifying one. This namespace is used to retreive either named mappings or full component paths.

| DSL | Description |
| :--- | :--- |
| empty | Same as saying id. Get a mapped instance with the same name as defined in the property, argument or setter method. |
| id | Get a mapped instance with the same name as defined in the property, argument or setter method. |
| id:{name} | Get a mapped instance by using the second part of the DSL as the mapping name. |
| id:{name}:{method} | Get the {name} instance object, call the {method} and inject the results |
| model | Get a mapped instance with the same name as defined in the property, argument or setter method. |
| model:{name} | Get a mapped instance by using the second part of the DSL as the mapping name. |
| model:{name}:{method} | Get the {name} instance object, call the {method} and inject the results |
| @module | Get the object from a specific module. The name of the alias is from the property used |

```javascript
// Let's assume we have mapped a few objects called: UserService, SecurityService and RoleService

// Empty inject, use the property name, argument name or setter name
property name="userService" inject;

// Using the name of the mapping as the value of the inject
property name="security" inject="SecurityService";

// Using the full namespace
property name="userService" inject="id:UserService";
property name="userService" inject="model:UserService";

// Simple factory method
property name="roles" inject="id:RoleService:getRoles";

// Module Injection Shortcut
property name="MyService" inject="@myModule";
```

## CFC Instantiation Order

When WireBox builds CFC instances, it is important to know the order of operations.  This controls when injected dependencies are available for you to use.

1. Component is instantiated with `createObject()`
2. CF automatically runs the pseudo constructor \(any code outside the a method declaration\)
3. The `init()` method is called \(if it exists\), passing any constructor args
4. Property \(mixin\) and setting injection happens
5. The `onDIComplete()` method is called \(if it exists\)

Based on that order, you can see that injected dependencies \(except constructor ones\) are not available yet to use in the `init()` and you must wait to use them in the `onDIComplete()` method.


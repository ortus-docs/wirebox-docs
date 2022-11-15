# Provider Namespace

Inject object providers, please refer to our [provider section](../../advanced-topics/providers/) in this guide.

| DSL                       | Description                                                                                               |
| ------------------------- | --------------------------------------------------------------------------------------------------------- |
| `provider`                | Build an object provider that will return the mapping according to the property, method or argument name. |
| `provider:{name}`         | Build an object provider that will return the {name} mapping.                                             |
| `provider:{injectionDSL}` | Build an object provider that will return the object that the {injectionDSL} refers to                    |

```javascript
// using id
property name="timedService" inject="provider:TimedService";

// using DSL
property name="timedService" inject="provider:logbox:logger:{this}";
```

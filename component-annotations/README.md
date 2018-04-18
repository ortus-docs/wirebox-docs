# Component Annotations

A part from using the configuration binder, you can also leverage component annotations to dictate behavior on the object.

| Annotation | Type | Description |
| --- | --- | --- |
| **autowire** | boolean | All objects are marked as autowire=true, so if you want to disable autowiring, you can add this annotation as false. You do NOT need to add this annotation if you want to autowire it, it is redundant if you do. |
| **alias** | string | A list of aliased names you can attach to a CFC instance apart from its Component name. This is great when using the `mapDirectory()` binder function. |
| **eagerInit** | none | All objects are lazy loaded unless they are marked with this annotation or marked as eager init in the binder configuration. |
| **threadSafe** | none or boolean | Determines the locking construction of the object for its wiring of dependencies. Please see our _Object Persistence & Thread Safety_ Section. |
| **scope** | string | A valid WireBox scope or a custom registered scope. Remember that ALL components by default are placed in the NO SCOPE scope. This means they are considered transient objects. |
| **singleton** | none | Marks a component as a singleton object. |
| **cachebox** | string | Marks a component to be stored in CacheBox. The value of this annotation should be a valid registered CacheBox cache provider. The default cache provider is called default |
| **cache** | boolean | Marks a component to be cached in CacheBox in the default provider. |
| **cacheTimeout** | numeric | The timeout in minutes when the object is stored in the CacheBox provider |
| **cacheLastAccessTimeout** | numeric | The timeout in minutes when the object is stored in the CacheBox provider |
| **mixins** | list | A list of UDF templates to mixin into the object |


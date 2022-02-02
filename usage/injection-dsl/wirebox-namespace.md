# WireBox Namespace

Talk and get objects from the current WireBox injector.

### 1st Level DSL

| DSL       | Description                             |
| --------- | --------------------------------------- |
| `wirebox` | Get a reference to the current injector |

### 2nd Level DSL

| DSL                      | Description                                                                                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `wirebox:asyncManager`   | Get a reference to the Async Manager                                                                                                                       |
| `wirebox:binder`         | Get a reference to the injector's binder                                                                                                                   |
| `wirebox:eventManager`   | Get a reference to injector's event manager                                                                                                                |
| `wirebox:objectMetadata` | Inject the target object's metadata struct                                                                                                                 |
| `wirebox:parent`         | Get a reference to the parent injector (if any)                                                                                                            |
| `wirebox:properties`     | Get the entire properties structure the injector is initialized with. If running within a ColdBox context then it is the structure of application settings |
| `wirebox:populator`      | Get a reference to a WireBox's Object Populator utility                                                                                                    |
| `wirebox:targetId`       | The target ID used when injecting the object                                                                                                               |

### 3rd Level DSL

| DSL                       | Description                                                  |
| ------------------------- | ------------------------------------------------------------ |
| `wirebox:child:{name}`    | Inject a child injector by name                              |
| `wirebox:property:{name}` | Retrieve one key of the properties structure                 |
| `wirebox:scope:{scope}`   | Get a direct reference to an internal or custom scope object |

```javascript
property name="beanFactory" inject="wirebox";
property name="settings" inject="wirebox:properties";
property name="singletonCache" inject="wirebox:scope:singleton";
property name="populator" inject="wirebox:populator";
property name="binder" inject="wirebox:binder";

// Child Injectors
property name="categoryService" inject="wirebox:child:childInjector"
```

### 4th Level DSL

| DSL                          | Description                                      |
| ---------------------------- | ------------------------------------------------ |
| `wirebox:child:{name}:{id}`  | Inject the `id` from the `named` child injector  |
| `wirebox:child:{name}:{dsl}` | Inject the `dsl` from the `named` child injector |

```javascript
property name="categoryService" inject="wirebox:child:childInjector:CategoryService"
property name="categoryService" inject="wirebox:child:childInjector:{DSL}"
```

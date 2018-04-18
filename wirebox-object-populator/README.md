# WireBox Object Populator

WireBox also comes packaged with our handy object populator that has been so successful in our ColdBox applications. The object populator object can populate objects with data from XML, JSON, WDDX, structures, queries and much more. So we highly encourage you to check it out as it will really help out in your applications.

The way to retrieve it is to use the `getObjectPopulator()` method on the injector and then call one of our populate methods on the object. You can also use the `wirebox:populator` injection DSL to retrieve it.

```javascript
populator = injector.getObjectPopulator();

property name="populator" inject="wirebox:populator";
```


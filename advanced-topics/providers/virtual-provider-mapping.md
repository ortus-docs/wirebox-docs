# Virtual Provider Mapping

You can also use our cool mapping DSL to create mappings that refer to provided objects by using the DSL construction type:

```javascript
// map an object to a virtual provided object
map("coolObjectProvider")
    .toDSL("provider:HardToConstructObject");

// map an object an set the explicit DI arguments or DI setters to virtual provided objects
map("SearchService")
    .to("model.search.SearchService")
    .initArg(name="searchCriteria",dsl="provider:requestCriteria");
```

You can use the following mapping methods to map to virtual providers by using their dsl arguments:

* `mapDSL()`
* `mapDSL()`
* `property(name="",dsl="")`
* `setter(name="",dsl="")`
* `methodArg(name="",dsl="")`

# Mapping Destinations

The mapping destinations tell WireBox what type of object you are mapping to. You will usually use these methods by concatenating `map()` or `with()` initiator calls:

| Method Signature | Description |
| :--- | :--- |
| `to(path)` | Maps a name to a CFC instantiation path |
| `toDSL(dsl)` | Maps a name to DSL builder string. Construction is done by using this DSL string \(Look at Injection DSL\) |
| `toFactoryMethod(factory,method)` | Maps a name to another mapping \(factory\) and its method call. If you would like to pass in parameters to this factory method call you will use the `methodArg()` DSL method concatenated to this method call |
| `toJava(path)` | Maps a name to a Java class that can be instantiated via `createObject("java")` |
| `toProvider(provider)` | Maps a name to another mapping \(provider\) that must implement the WireBox Provider interface \(`coldbox.system.ioc.IProvider`\) |
| `toRSS(path)` | Maps a name to an atom or RSS URL. WireBox will then use the `cffeed` tag to construct this RSS feed. It builds out into a structure with two keys: **metadata** : The metadata of the feed **items** : The items in the feed |
| `toValue(value)` | Maps a name to a constant value, which can be ANYTHING. |
| `toWebservice(path)` | Maps a name to a webservice WSDL URL. WireBox will create the webservice via `createObject("webservice")` for you. |

Here are some examples:

```javascript
// CFC
map("FunkyObject").to("myapp.model.service.FunkyService");
mapPath("myapp.model.service.FunkyService");
mapDirectory("myapp.model");
// Java
map("buffer").toJava("java.lang.StringBuffer");
// RSS feed
map("googleNews").toRSS("http://news.google.com/news?output=rss");
// Webservice
map("myWS").toWebservice("http://myapp.com/app.cfc?wsdl");
// Provider
map("Espresso").toProvider("FunkyEspressoProvider");
// DSL
map("Logger").toDSL("logbox:root");

// factory methods
map("ColdboxFactory").to("coldbox.system.extras.ColdboxFactory");
map("ColdBoxController").toFactoryMethod(factory="ColdBoxFactory",method="getColdBox");
map("BeanInjector")
    .toFactoryMethod(factory="ColdBoxFactory",method="getPlugin")
    .methodArg(name="plugin",value="BeanFactory")

// Mixin a new method in my object that dispenses users
mapPath("UserService")
    .providerMethod("getUser","User");
```

> **Caution** Please note that WireBox can create different types of objects for DI. However, only CFCs will be inspected for autowiring automatically unless you specifically tell WireBox that a certain mapping should not be autowired. In this case you will use the dependencies DSL to define all DI relationships.


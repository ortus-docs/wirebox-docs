# Persistence DSL

The next step in our mapping DSL excursion is to learn about how WireBox will persist these object mappings into WireBox scopes. By default (as we have seen), all object mappings are transient objects and they belong to a scope type called **NOSCOPE**.

However, we need to specifically tell WireBox into what scope the declared mapped objects should be placed on in order for us to leverage caching, the singleton pattern, etc. This is accomplished by leveraging our persistence component annotations or the following methods if you prefer a non-annotation approach:

> **Note** Please note that all WireBox configuration binders have two public properties:

```javascript
this.TYPES - Enum class (coldbox.system.ioc.Types)
this.SCOPES - Enum class (coldbox.system.ioc.Scopes)
```

These classes have on themselves several public properties that are a cool shorthand way to link to construction types or persistence scopes

| Method Signature                                                                           | Description                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **asSingleton**()                                                                          | Maps an object to the WireBox internal Singleton scope                                                                                                                                                                            |
| **into**(scope)                                                                            | Maps an object to a valid WireBox internal scope or any custom registered scopes by using the registered scope name. Valid internal WireBox scopes are:  NOSCOPE PROTOTYPE SINGLETON SESSION APPLICATION REQUEST SERVER  CACHEBOX |
| **inCacheBox**(\[key='mappingName'],\[timeout],\[lastAccessTimeout],\[provider='default']) | Maps an object to the integrated [CacheBox](https://github.com/ortus/wirebox-documentation/tree/b9a6ae3e91f7dcb74ec7e900e27243e19824cf27/mapping\_dsl/wiki/CacheBox.cfm) instance                                                 |
| **asEagerInit()**                                                                          | Maps an object to be created immediately once the Injector is created. By default all object mappings are lazy loaded in construction.                                                                                            |

So just remember that these persistence DSL methods are not mandatory. If you are an annotations kinda developer, then you can easily add these persistence annotations to your classes.

```javascript
// CFC
map("FunkyObject")
    .to("myapp.model.service.FunkyService")
    .asSingleton();
mapPath("myapp.model.service.FunkyService")
    .into(this.SCOPES.REQUEST);
// Java as NO SCOPE
map("buffer").toJava("java.lang.StringBuffer");
// RSS feed
map("googleNews")
    .toRSS("http://news.google.com/news?output=rss")
    .inCacheBox(timeout=60,lastAccessTimeout=15);
// Webservice
map("myWS")
    .toWebservice("http://myapp.com/app.cfc?wsdl")
    .into(this.SCOPES.APPLICATION);
```

{% hint style="danger" %}
**Caution** Please note that by leveraging scopes that can expire such as cachebox,request,session,applications,etc you must take into account the way they are injected into other objects. They can experience a DI side effect called scope widening injection that can link an object reference that expires into another object reference that does not expire (like singleton). This causes nasty side effects and issues, so please refer to the WireBox Providers section to find out how you can avoid this nasty pitfall by using WireBox providers.
{% endhint %}

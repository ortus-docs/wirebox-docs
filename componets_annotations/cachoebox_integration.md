# CachoeBox Integration

If you would like to use CacheBox for persistence for you objects you will need to mark your CFC with the following annotation(s)

* cachebox="[provider]" - The default provider is called 'default', so this annotation can be empty or a named cache provider
* cache - Cache into the default provider, shorthand annotation, no value needed

This annotation has two sub annotations that you can also leverage for granular control of your CacheBox integration:

* cacheTimeout - The timeout in minutes (optional)
* cacheLastAccessTimeout - The last access or idle timeout in minutes (optional)

```javascript
// cache into the default provider
component cache{}
// cache into the default provider
component cachebox{}

// cache into the ehcache provider
component cachebox="ehcache"{}

// cache into the ehcache provider with settings
component cachebox="ehcache" cacheTimeout="20"{}

// cache with settings
component cache cacheTimeout="60" cacheLastAccessTimeout="10"{}
```
<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="12%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Important : When storing objects in volatile scopes like cache, session, request, etc. You must be careful of not injecting them directly into singletons or other volatile objects as you could have memory leaks via a side effect called Scope Widening Injection. We recommend combining them via WireBox Providers to avoid this side effect. </b></p>
<div style="clear:both"></div>
</div>

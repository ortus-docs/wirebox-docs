---
description: June 21, 2022
---

# What's New With 6.7.0

## Major Updates

Here is a listing of all the major updates and improvements in this version.

### WireBox Performance, Performance and More Performance

![Performance, stopwatch, timer, speed, time, time management](https://cdn2.iconfinder.com/data/icons/thin-line-icons-for-seo-and-development-1/64/SEO\_stopwatch\_timer\_performance-128.png)

This release brings in a complete re-architecture of the creation, inspection and wiring of objects in WireBox in order to increase performance.  Every single line of code was optimized and analyzed in order to bring the creation, inspection and wiring of objects to its maximum speed.  This will be noted more on the creation of transient (non-persisted) objects more than in singleton objects.  So if you are asking WireBox for transient objects, you will see and feel the difference.

In some of our performance testing we had about 4000 object instantiations running between 500ms-1,100 ms depending on CPU load. While with simple `createObject()`  and no wiring, they click around 400-700 ms.  Previously, we had the same instantiations clocking at 900-3,500 ms.  So we can definitely see a major improvement in this area.

## Release Notes

{% tabs %}
{% tab title="WireBox" %}
**Bug**

* [WIREBOX-126](https://ortussolutions.atlassian.net/browse/WIREBOX-126) Inherited Metadata Usage - Singleton attribute evaluated before Scopes

**Improvement**

* [WIREBOX-129](https://ortussolutions.atlassian.net/browse/WIREBOX-129) Massive refactor to improve object creation and injection wiring
* [WIREBOX-128](https://ortussolutions.atlassian.net/browse/WIREBOX-128) Injector now caches all object contains lookups to increase performance across hierarchy lookups
* [WIREBOX-127](https://ortussolutions.atlassian.net/browse/WIREBOX-127) Lazy load all constructs on the Injector to improve performance
* [WIREBOX-125](https://ortussolutions.atlassian.net/browse/WIREBOX-125) Remove the usage of identity hash codes, they are no longer relevant and can cause contention under load
{% endtab %}

{% tab title="CacheBox" %}
**Bug**

* [CACHEBOX-66](https://ortussolutions.atlassian.net/browse/CACHEBOX-66) Cachebox concurrent store meta index not thread safe during reaping

**Improvement**

* [CACHEBOX-82](https://ortussolutions.atlassian.net/browse/CACHEBOX-82) Remove the usage of identity hash codes, they are no longer relevant and can cause contention under load
{% endtab %}

{% tab title="LogBox" %}
**Improvement**

* [LOGBOX-68](https://ortussolutions.atlassian.net/browse/LOGBOX-68) Remove the usage of identity hash codes, they are no longer relevant and can cause contention under load
* [LOGBOX-65](https://ortussolutions.atlassian.net/browse/LOGBOX-65) File Appender missing text "ExtraInfo: "
{% endtab %}
{% endtabs %}

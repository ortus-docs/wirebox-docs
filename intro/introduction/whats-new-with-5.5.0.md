# What's New With 6.2.0

This minor release brings in some major performance enhancements for the way WireBox maps and creates objects.  We highly encourage upgrading to it.

{% embed url="https://coldbox.ortusbooks.com/intro/release-history/whats-new-with-6.2.0" %}
What's New With ColdBox 6.2.0
{% endembed %}

## Release Notes

{% tabs %}
{% tab title="WireBox" %}
### Bugs

* \[[WIREBOX-99](https://ortussolutions.atlassian.net/browse/WIREBOX-99)] - parameter \[binder] to function \[process] is required but was not passed in When setting coldbox.autoMap to false and choosing either method of mapping a directory:
* \[[WIREBOX-102](https://ortussolutions.atlassian.net/browse/WIREBOX-102)] - ACF incompats with future combinations due to dumb elvis operator bug

### New Features

* \[[WIREBOX-98](https://ortussolutions.atlassian.net/browse/WIREBOX-98)] - Pass the current `injector` to the binder's life-cycle methods: `onShutdown(), onLoad()`
* \[[WIREBOX-100](https://ortussolutions.atlassian.net/browse/WIREBOX-100)] - Create a `processEagerInits()` so it can process them at wirebox load
* \[[WIREBOX-101](https://ortussolutions.atlassian.net/browse/WIREBOX-101)] - Complete rewrite of the `Mapping` object to script and performance optimizations
* \[[WIREBOX-103](https://ortussolutions.atlassian.net/browse/WIREBOX-103)] - Complete rewrite of the WireBox `Binder` to script and optimizations
* \[[WIREBOX-104](https://ortussolutions.atlassian.net/browse/WIREBOX-104)] - New WireBox config: `autoProcessMappings` which can be used to auto process metadata inspections on startup.
{% endtab %}

{% tab title="CacheBox" %}
### Improvements

* \[[COLDBOX-945](https://ortussolutions.atlassian.net/browse/COLDBOX-945)] - Event caching now bases off the multi host key from the event.getSESBaseURL() to improve consistencies and single responsibility
* \[[COLDBOX-953](https://ortussolutions.atlassian.net/browse/COLDBOX-953)] - Update `DateFormat` Mask to use lowercase "d" to be compatible with ACF2021
{% endtab %}

{% tab title="LogBox" %}
### Bugs

* \[[LOGBOX-56](https://ortussolutions.atlassian.net/browse/LOGBOX-56)] - Missing line break on file appender control string

### New Features

* \[[LOGBOX-57](https://ortussolutions.atlassian.net/browse/LOGBOX-57)] - new `shutdown()` method to process graceful shutdown of LogBox
* \[[LOGBOX-58](https://ortussolutions.atlassian.net/browse/LOGBOX-58)] - New logbox config `onShutdown()` callback, which is called when LogBox has been shutdown
* \[[LOGBOX-59](https://ortussolutions.atlassian.net/browse/LOGBOX-59)] - New `shutdown()` method can be now used in appenders that will be called when LogBox is shutdown
{% endtab %}
{% endtabs %}

##

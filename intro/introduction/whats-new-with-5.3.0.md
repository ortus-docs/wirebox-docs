# What's New With 6.0.0

WireBox 6 is a major release for WireBox accompanied by the ColdBox Platform release.  WireBox includes LogBox and CacheBox and you can find the appropriate release notes for those libraries as well.

{% embed url="https://coldbox.ortusbooks.com/intro/release-history/whats-new-with-6.0.0" %}
What's New With 6.0.0
{% endembed %}

## Release Notes

{% tabs %}
{% tab title="WireBox" %}
### Bugs

* \[[WIREBOX-90](https://ortussolutions.atlassian.net/browse/WIREBOX-90)] - Fix constructor injection with virtual inheritance

### New Features

* \[[WIREBOX-91](https://ortussolutions.atlassian.net/browse/WIREBOX-91)] - Injector's get a reference to an asyncManager and a task scheduler whether they are in ColdBox or non-ColdBox mode
* \[[WIREBOX-92](https://ortussolutions.atlassian.net/browse/WIREBOX-92)] - New \`executors\` dsl so you can easily inject executors ANYWEHRE
* \[[WIREBOX-97](https://ortussolutions.atlassian.net/browse/WIREBOX-97)] - New dsl coldbox:coldboxSetting:{setting} alias to coldbox:fwSetting:{setting}

### Improvements

* \[[WIREBOX-88](https://ortussolutions.atlassian.net/browse/WIREBOX-88)] - Improve WireBox error on Adobe CF
* \[[WIREBOX-93](https://ortussolutions.atlassian.net/browse/WIREBOX-93)] - Rename WireBox provider get() to $get() to avoid conflicts with provided classes
* \[[WIREBOX-94](https://ortussolutions.atlassian.net/browse/WIREBOX-94)] - getInstance() now accepts either dsl or name via the first argument and initArguments as second argument
{% endtab %}

{% tab title="CacheBox" %}
### Bugs

* \[[CACHEBOX-59](https://ortussolutions.atlassian.net/browse/CACHEBOX-59)] - Announced Events in the set() of the cacheBoxProvider
* \[[CACHEBOX-63](https://ortussolutions.atlassian.net/browse/CACHEBOX-63)] - cfthread-20506;variable \[ATTRIBUES] doesn't exist;lucee.runtime.exp.ExpressionException: variable \[ATTRIBUES] doesn't exist

### New Features

* \[[CACHEBOX-24](https://ortussolutions.atlassian.net/browse/CACHEBOX-24)] - CacheBox reaper : migrate to a scheduled task via cbPromises
* \[[CACHEBOX-60](https://ortussolutions.atlassian.net/browse/CACHEBOX-60)] - CacheFactory gets a reference to an asyncManager and a task scheduler whether they are in ColdBox or non-ColdBox mode

### Improvements

* \[[CACHEBOX-64](https://ortussolutions.atlassian.net/browse/CACHEBOX-64)] - Migrations to script and more fluent programming
{% endtab %}

{% tab title="LogBox" %}
### Bugs

* \[[LOGBOX-35](https://ortussolutions.atlassian.net/browse/LOGBOX-35)] - FileAppender: if logging happens in a thread, queue never gets processed and, potentially, you run out of heap space
* \[[LOGBOX-38](https://ortussolutions.atlassian.net/browse/LOGBOX-38)] - Rotate property is defined but never used
* \[[LOGBOX-45](https://ortussolutions.atlassian.net/browse/LOGBOX-45)] - Work around for adobe bug CF-4204874 where closures are holding on to tak contexts
* \[[LOGBOX-50](https://ortussolutions.atlassian.net/browse/LOGBOX-50)] - Rolling file appender inserting tabs on first line

### New Features

* \[[LOGBOX-5](https://ortussolutions.atlassian.net/browse/LOGBOX-5)] - Allow config path as string in LogBox init (standalone)
* \[[LOGBOX-11](https://ortussolutions.atlassian.net/browse/LOGBOX-11)] - Allow standard appenders to be configured by name (instead of full path)
* \[[LOGBOX-36](https://ortussolutions.atlassian.net/browse/LOGBOX-36)] - Added an \`err()\` to abstract appenders for reporting to the error streams
* \[[LOGBOX-42](https://ortussolutions.atlassian.net/browse/LOGBOX-42)] - All appenders get a reference to the running LogBox instance
* \[[LOGBOX-43](https://ortussolutions.atlassian.net/browse/LOGBOX-43)] - LogBox has a scheduler executor and the asyncmanager attached to it for standalone and ColdBox mode.
* \[[LOGBOX-44](https://ortussolutions.atlassian.net/browse/LOGBOX-44)] - Rolling appender now uses the new async schedulers to stream data to files
* \[[LOGBOX-46](https://ortussolutions.atlassian.net/browse/LOGBOX-46)] - Update ConsoleAppender to use TaskScheduler
* \[[LOGBOX-47](https://ortussolutions.atlassian.net/browse/LOGBOX-47)] - AbstractAppender log listener and queueing facilities are now available for all appenders
* \[[LOGBOX-48](https://ortussolutions.atlassian.net/browse/LOGBOX-48)] - DB Appender now uses a queueing approach to sending log messages
* \[[LOGBOX-49](https://ortussolutions.atlassian.net/browse/LOGBOX-49)] - Rolling File Appender now uses the async scheduler for log rotation checks

### Improvements

* \[[LOGBOX-37](https://ortussolutions.atlassian.net/browse/LOGBOX-37)] - Improvements to threading for logging to avoid dumb Adobe duplicates
* \[[LOGBOX-41](https://ortussolutions.atlassian.net/browse/LOGBOX-41)] - refactoring of internal utility closures to udfs to avoid ACF memory leaks: CF-4204874
* \[[LOGBOX-51](https://ortussolutions.atlassian.net/browse/LOGBOX-51)] - Migrations to script and more fluent programming
{% endtab %}
{% endtabs %}

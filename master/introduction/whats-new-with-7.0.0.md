---
description: Discover the power of WireBox 7.0.0
---

# What's New With 7.0.0

You can read all about this release on our main What's New Page: [https://coldbox.ortusbooks.com/readme/release-history/whats-new-with-7.0.0](https://coldbox.ortusbooks.com/readme/release-history/whats-new-with-7.0.0)

### Release Notes

The full release notes per library can be found below. Just click on the library tab and explore their release notes:

{% tabs %}
{% tab title="WireBox" %}
### Improvement

[WIREBOX-133](https://ortussolutions.atlassian.net/browse/WIREBOX-133) BeanPopulator renamed to ObjectPopulator to be consistent with naming

### Bug

[WIREBOX-132](https://ortussolutions.atlassian.net/browse/WIREBOX-132) WireBox caches Singletons even if their autowired dependencies throw exceptions.

### New Feature

[WIREBOX-89](https://ortussolutions.atlassian.net/browse/WIREBOX-89) Wirebox - add onInjectorMissingDependency event

[WIREBOX-130](https://ortussolutions.atlassian.net/browse/WIREBOX-130) Ability to remove specific objects from wirebox injector singleton's and request scopes via a \`clear( key )\` method

[WIREBOX-131](https://ortussolutions.atlassian.net/browse/WIREBOX-131) Object Delegators

[WIREBOX-134](https://ortussolutions.atlassian.net/browse/WIREBOX-134) Object Populator is now created by the Injector and it is now a singleton

[WIREBOX-135](https://ortussolutions.atlassian.net/browse/WIREBOX-135) Object populator now caches orm entity maps, so they are ONLy loaded once and population with orm objects accelerates tremendously

[WIREBOX-136](https://ortussolutions.atlassian.net/browse/WIREBOX-136) object populator cache relational metadata for faster population of the same objects

[WIREBOX-137](https://ortussolutions.atlassian.net/browse/WIREBOX-137) New \`this.population\` marker for controlling mas population of objects. It can include an \`include\` and and \`exclude\` list.

[WIREBOX-138](https://ortussolutions.atlassian.net/browse/WIREBOX-138) Lazy Properties

[WIREBOX-139](https://ortussolutions.atlassian.net/browse/WIREBOX-139) Property Observers

[WIREBOX-140](https://ortussolutions.atlassian.net/browse/WIREBOX-140) Transient request cache for injections and delegations

[WIREBOX-141](https://ortussolutions.atlassian.net/browse/WIREBOX-141) New config setting transientInjectionCache to enable or disable globally, default is true

[WIREBOX-142](https://ortussolutions.atlassian.net/browse/WIREBOX-142) You can now instantiate an Injector with the \`binder\` argument being the config structure instead of creating a binder

[WIREBOX-143](https://ortussolutions.atlassian.net/browse/WIREBOX-143) New injection DSL for ColdBox Root Injector \`coldbox:rootWireBox\`

[WIREBOX-144](https://ortussolutions.atlassian.net/browse/WIREBOX-144) Injectors can now track the root injector by having a root reference via \`getRoot(), hasRoot()\` methods

[WIREBOX-145](https://ortussolutions.atlassian.net/browse/WIREBOX-145) New DSL for wirebox only root injectors: \`wirebox:root\`
{% endtab %}

{% tab title="CacheBox" %}
### Bug

* [CACHEBOX-83](https://ortussolutions.atlassian.net/browse/CACHEBOX-83) Intermittent Exception from MetadataIndexer
{% endtab %}

{% tab title="LogBox" %}
### Improvement

[LOGBOX-67](https://ortussolutions.atlassian.net/browse/LOGBOX-67) Come up with better default serialization for exception objects on LogEvents

### New Feature

[LOGBOX-61](https://ortussolutions.atlassian.net/browse/LOGBOX-61) Allow for closure for all logging messages in the logger, this way, we can verify the logging level automatically.

[LOGBOX-69](https://ortussolutions.atlassian.net/browse/LOGBOX-69) LogEvents in JSON are now prettified
{% endtab %}
{% endtabs %}

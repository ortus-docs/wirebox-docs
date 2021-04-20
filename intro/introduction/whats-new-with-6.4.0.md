# What's New With 6.4.0

Here are the release notes for WireBox 6.4.0

{% tabs %}
{% tab title="WireBox" %}
#### Bugs

* [WIREBOX-112](https://ortussolutions.atlassian.net/browse/WIREBOX-112) virtual inheritance causes double `inits` on objects that do not have a constructor and their parent does.
* [WIREBOX-95](https://ortussolutions.atlassian.net/browse/WIREBOX-95) `onDIComplete`\(\) is called twice using virtual inheritance

#### New Features

* [WIREBOX-114](https://ortussolutions.atlassian.net/browse/WIREBOX-114) New coldbox dsl =&gt; `coldbox:appScheduler` which gives you the `appScheduler@coldbox` instance
* [WIREBOX-113](https://ortussolutions.atlassian.net/browse/WIREBOX-113) new injection dsl: `wirebox:asyncManager`
{% endtab %}
{% endtabs %}


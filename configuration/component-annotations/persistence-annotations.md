# Persistence Annotations

The following annotations can be placed in the class declaration to tell the WireBox injector where to persist the constructed object. If no scope annotations are found on the class or mappings then the object is treated as **NO SCOPE** or a prototype/transient object; one that gets constructed and discarded every time.

* `singleton` - A singleton object that persists for the entire life-time of the application
* `scope="registered_scope"` : Persist in a registered scope: session, request, singleton, custom, etc.
* `transientCache` : Enable/disable per-request transient injection caching for this mapping (defaults to true)

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class singleton{}

class scope="singleton"{}

class scope="request"{}

class singleton threadsafe{}

class transientCache="false"{}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component singleton{}

component scope="singleton"{}

component scope="request"{}

component singleton threadsafe{}

component transientCache="false"{}
```
{% endtab %}
{% endtabs %}

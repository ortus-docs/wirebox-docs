# Installing WireBox

WireBox can be installed as a standalone framework or included with the latest ColdBox Platform release, so it is unnecessary if you are within a ColdBox application.

## Supported Languages

WireBox supports both **BoxLang** (preferred) and **CFML** (ColdFusion Markup Language):

| Language | Extensions | Notes |
| --- | --- | --- |
| **BoxLang** | `.bx`, `.bxm`, `.bxs` | Preferred — modern JVM language, owned by the ColdBox team |
| **CFML** | `.cfc`, `.cfm` | Fully supported for existing applications |

## System Requirements

* **BoxLang** 1+ (Preferred)
* **Adobe ColdFusion** 2023+
* **Lucee** 6+

## Standalone Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of WireBox with a simple command:

```bash
# Latest Version
box install wirebox

# Bleeding Edge
box install wirebox@be
```

This will install WireBox as a dependency in your application into a folder called `wirebox`. You can then leverage the standalone namespace within your application: `wirebox.system.ioc`.

### Mappings

You will need the following mapping that points to the folder you installed `wirebox` into:

{% tabs %}
{% tab title="BoxLang" %}
```bx
// Application.bx
this.mappings[ "/wirebox" ] = expandPath( "path/to/wirebox" );
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// Application.cfc
this.mappings[ "/wirebox" ] = "path.to.wirebox";
```
{% endtab %}
{% endtabs %}

This will ensure that the appropriate libraries can find each other.

{% hint style="danger" %}
Remember that this only applies to the standalone approach.
{% endhint %}

## Namespaces

### Standalone Namespace

`wirebox.system.ioc`

![](<../.gitbook/assets/installing_WireBoxSystem (1).jpg>)

### ColdBox Namespace

`coldbox.system.ioc`

![](<../.gitbook/assets/installing_ColdBoxSystem (1).jpg>)

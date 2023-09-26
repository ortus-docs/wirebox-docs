# Installing WireBox

WireBox can be installed as a standalone framework or included with the latest ColdBox Platform release, so it is unnecessary if you are within a ColdBox application.

## System Requirements

* Adobe ColdFusion 2018+
* Lucee 5+

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

You will need the following mappings that all point to the folder you installed `wirebox` into:

```cfscript
this.mappings[ "/wirebox" ] = 
    this.mappings[ "/cachebox" ] = 
    this.mappings[ "/logbox" ] =  
    "path.to.wirebox";
```

This will ensure that the appropriate libraries can find each other.

{% hint style="danger" %}
Remember that this only applies to the standalone approach.
{% endhint %}

## Manual Download

You can download the latest version of WireBox from [https://www.forgebox.io/view/wirebox](https://www.forgebox.io/view/wirebox?filter=stable#versions). Place in your webroot or create a `/wirebox` mapping in your system.

## Namespaces

### Standalone Namespace

`wirebox.system.ioc`

![](<../.gitbook/assets/installing\_WireBoxSystem (1).jpg>)

### ColdBox Namespace

`coldbox.system.ioc`

![](../.gitbook/assets/installing\_ColdBoxSystem.jpg)

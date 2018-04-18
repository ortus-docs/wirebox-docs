# Installing WireBox

WireBox can be downloaded as a standalone framework or it is included with the latest ColdBox Platform release, so no need to install it if you are within a ColdBox application.

{% hint style="info" %}
The best way to install LogBox is using **CommandBox CLI and package manager.**
{% endhint %}

## System Requirements

* Adobe ColdFusion 11+
* Lucee 4.5+

## CommandBox Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of WireBox with a simple command:

```bash
# Latest Version
box install wirebox

# Bleeding Edge
box install wirebox@be
```

This will install Wirebox as a dependency in your application into a folder called `wirebox`. You can then leverage the standalone namespace within your application: `wirebox.system.ioc`.

## Manual Download

You can download the latest version of WireBox from [https://www.coldbox.org/download\#wirebox](https://www.coldbox.org/download#wirebox). Place in your webroot or create a `/wirebox` mapping in your system.


## Namespaces

### Standalone Namespace

`wirebox.system.ioc`

![](.gitbook/assets/installing_wireboxsystem.jpg)

### ColdBox Namespace

`coldbox.system.ioc`

![](.gitbook/assets/installing_coldboxsystem.jpg)



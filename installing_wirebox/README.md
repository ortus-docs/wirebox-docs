# Installing WireBox

WireBox can be downloaded as a standalone framework or it is included with the latest ColdBox Platform release. The main difference between both versions is the instantiation and usage namespace, the rest is the same.

* [Download WireBox Standalone](http://www.coldbox.org/download)
* [Download API Docs](http://www.coldbox.org/api)


## Manual Installation

If you are using WireBox within a ColdBox application context, then WireBox is part of the platform. Just install ColdBox normally. If you are using WireBox standalone, just drop WireBox in your application root or create a mapping called `wirebox` that points to the installation folder. If you can run the following snippet, then WireBox is installed correctly:

```
wirebox = new wirebox.system.ioc.Injector();
```

> **Note** Please remember that if you use the standalone version the namespace is `wirebox.system.ioc` and if you use the ColdBox application version it is `coldbox.system.ioc`. From this point on, we will use the standalone namespace for simplicity.
<br>


## CommandBox Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of WireBox with a simple command:

```bash
box install wirebox
```

You can then leverage the standalone namespace within your application: `wirebox.system.ioc`



## Standalone Namespace

`wirebox.system.ioc`

<br>
<img src="../images/installing_WireBoxSystem.jpg">
<br>
<br>

## ColdBox Namespace

`coldbox.system.ioc`

<br>
<img src="../images/installing_ColdBoxSystem.jpg">

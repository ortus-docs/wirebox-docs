# Installation

If you are using WireBox within a ColdBox application context, then WireBox is part of the platform. Just install ColdBox normally. If you are using WireBox standalone, just drop WireBox in your application root or create a mapping called `wirebox` that points to the installation folder. If you can run the following snippet, then WireBox is installed correctly:

```
wirebox = new wirebox.system.ioc.Injection(); 
```

<br>
<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="13%" style="float:left;margin-top:10px"><p style="margin:12px"><b> Note: Please remember that if you use the standalone version the namespace is wirebox.system.ioc and if you use the ColdBox application version it is coldbox.system.ioc. From this point on, we will use the standalone namespace for simplicity.</b></p>
<div style="clear:both"></div>
</div>
<br>


# CommandBox
You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of WireBox

```bash
box install wirebox
```
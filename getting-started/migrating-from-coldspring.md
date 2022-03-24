---
description: Easily migrate from ColdSpring to WireBox
---

# Migrating From ColdSpring

If you have an application that leveraged ColdSpring for your dependency injection, you can easily port it to WireBox.  The first step is converting the ColdSpring XML file to a WireBox Binder.  This will translate 1-1 the bean configurations to WireBox configurations.

Then it will be up to you to test your objects and get up and running really quickly.

### CommandBox

Make sure you have CommandBox CLI installed as we will be using it to convert our XML file to WireBox DSL.

{% embed url="https://www.ortussolutions.com/products/commandbox#download" %}
Download CommandBox
{% endembed %}

### ColdSpring XML to WireBox DSL

Now it's time to install our module that converts ColdSpring XML to WireBox DSL:

```bash
box install commandbox-coldspring-to-wirebox
```

Now it's time to convert your XML:

```bash
# Produces a WireBox.cfc where you run the command
coldspring-to-wirebox tests/coldspring.xml.cfm

# Stores the WireBox.cfc in the same location as the file above
coldspring-to-wirebox tests/coldspring.xml.cfm tests/WireBox.cfc
```

That's it!  This will convert all your definitions and you are ready to roll!

### Test Your Binder

We can now instantiate a new instance of WireBox with this Binder and use it!

```java
new wirebox.system.ioc.Injector( "tests/WireBox" );

// Get an instance!
application.wirebox.getInstance( "MyOldBean" );
```

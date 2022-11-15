---
description: Easily migrate from ColdSpring to WireBox
---

# Migrating From ColdSpring

ColdSpring was the first dependency injection framework for ColdFusion in the good 'ol days. It was inspired by Java Spring and it rocked during its tenure. As a matter of fact, there is still quite a large number of applications leveraging it, even though the framework itself is completely legacy, unsupported and might not even work on some versions of Adobe 2018+ as well. If you are in this technical debt boat and want a **quick win** and recover some ground in the technical debt war, then this document is for you.

If you have an application that leveraged ColdSpring for your dependency injection, you can easily port it to WireBox.  The first step is converting the ColdSpring XML file to a WireBox Binder.  This will translate 1-1 the bean configurations to WireBox configurations.

Then it will be up to you to test your objects and get up and running really quickly.

### WireBox

WireBox is an enterprise ColdFusion Dependency Injection and Aspect Oriented Programing (AOP) framework. WireBox's inspiration has been based on the idea of rapid workflows when building object oriented ColdFusion applications, programmatic configurations and simplicity. With that motivation we introduced dependency injection by annotations and conventions, which has been the core foundation of WireBox.

**WireBox is standalone framework for ColdFusion (CFML) applications and it is also bundled with the ColdBox Platform.**

![](https://www.ortussolutions.com/modules\_app/contentbox-custom/\_themes/ortus-2019/resources/assets/images/services/ninja.svg)

What's even more important its that WireBox is:

* Modern
* [Professionally Supported](https://www.ortussolutions.com/services/support)
* Actively Maintained
* Widely Used

### CommandBox

Make sure you have CommandBox CLI installed as we will be using it to [install WireBox](installing-wirebox.md) and convert our XML file to WireBox DSL.

{% embed url="https://www.ortussolutions.com/products/commandbox#download" %}
Download CommandBox
{% endembed %}

### ColdSpring XML to WireBox DSL

Now it's time to install our module that converts ColdSpring XML to WireBox DSL:

```bash
box install commandbox-coldspring-to-wirebox
```

This will install the `coldspring-to-wirebox` command into your CLI. You can get help by issuing a `coldspring-to-wirebox --help` command. However, it's very easy to use, so let's convert that XML file:

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

Right now would be a great time to create some canary integration tests using [TestBox](https://testbox.ortusbooks.com/) which can verify that your objects can be created and wired up correctly. This will be a huge help to get you started on the road to better test coverage and migrating your legacy elephant to modern times:

{% code title="UserServiceSpec.cfc" %}
```javascript
component extends="testbox.system.BaseSpec"{

     // executes before all suites
     function beforeAll(){
          wirebox = new wirebox.system.ioc.Injector( "path.to.Binder" );
     }

     // executes after all suites
     function afterAll(){
          structDelete( application, "wirebox" );
     }

     // All suites go in here
     function run( testResults, testBox ){
          describe( "UserService", () => {

               it( "can be created and wired", () => {
                    var target = wirebox.getInstance( "UserService" );
                    expect( target ).toBeComponent();
                    expect( target.getUserDAO() ).toBeComponent();
               } );

          } );
     }

}
```
{% endcode %}

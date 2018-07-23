# Getting Jiggy Wit It!

## A primer to WireBox usage

Dependency injection and instance construction with WireBox is easy. In its most simplest form we can just leverage annotations and be off to dancing Big Willy style! You can use our global injection annotation inject on `cfproperties`, setter methods or constructor arguments. This annotation tells WireBox to inject something in place of the property, argument or method; basically it is your code shouting **"Hey buddy, I need your help here"**.

What it injects depends on the contents of this annotation that leverages our [injection DSL](../../usage/injection-dsl/) \(Domain Specific Language\). The simplest form of the DSL is to just tell WireBox what mapping to bring in for injection. Please note that I say mapping and not object directly, because WireBox works on the concept of an object mapping. This mapping in all reality can be a CFC, a java object, an RSS feed, a webservice, a constant value or pretty much anything you like.

If you don't like annotations because you feel they are too intrusive to your taste, don't worry, we also have a programmatic configuration binder you can use to define all your objects and their dependencies. We will discuss object mappings and our configuration binders later on, so let's look at how cool this is by checking out our Coffee Shop sample class. The `CoffeeShop` class below will use our three types of injections to showcase how WireBox works, please note that most likely we would build this class by picking one or the other, which in itself brings in pros and cons for each approach.

```javascript
component name="CoffeeShop" singleton{

// define a property and tell WireBox to inject it
property name="espressoMachine" inject="id:espressoMachine";

    function init(any owner inject){
        variables.owner = arguments.owner;
        return this;
    }

    function openShop() onDiComplete{
        espressoMachine.turnOn();
        owner.nap();
    }

    function setCashRegister(cashRegister) inject="id"{
        variables.cashRegister= arguments.cashRegister;
    }

    function makeEspresso(){
        return espressoMachine.makeEspresso();
    }
}
```

So let's break this class down. First, you can see a singleton annotation on the component declaration. This tells WireBox that this class should only be created once and then cached in its internal singleton scope of the injector. In other words, this is called object life scopes. You can refer to the persistence scopes annotations later on in the guide to learn all about how to scope your classes.

Second, we built our coffee shop class with three external dependencies: 1 by cfproperty, 1 by constructor argument and 1 by setter injection. Again, you can see later on in this guide the difference between all these injection styles and choose what you prefer. In this example, we just showcase the different injection styles. Also, as you can see from the source code the three types of injection uses the inject annotation but with different content:

```javascript
1. property name="espressoMachine" inject="id:espressoMachine";
2. function init(any owner inject)
3. function setCashRegister(cashRegister) inject="id"
```

If you just mark a property, argument or method with the inject annotation, WireBox will assume it is a mapping and the ID should be either the property name, the argument name or the method name. However, if you want to specify the id in the DSL string, just use the simple `id:{mapping}` dsl notation. That's it! Isn't that cool, you just mark out your dependencies and WireBox will build and inject them for you!

Thirdly, this class has the following method:

```javascript
function openShop() onDIComplete{
    espressoMachine.turnOn();
    owner.nap();
}
```

```markup
// or
<cffunction name="openShop" returnType="void" output="false" onDIComplete>
</cffunction>
```

The method has a cool little annotation called `onDIComplete` that tells WireBox that after all DI dependencies have been injected, then execute the method. That is so cool, WireBox can even open the coffee shop for me so I can get my espresso fix. Not only that but you can have multiple `onDIComplete` methods declared and WireBox will call them for you \(in discovered order\). These are called object post processors that are discovered by annotations or can be configured via our configuration binder and we will learn about them later on. WireBox also fires a series of object life cycle events throughout an object's life span in which you can build listens to and actually perform some cool stuff on them. So now that we got all excited about opening the coffee shop let's get into something even more interesting, unit testing and mocking.

Another important aspect leveraging DI concepts when building our components is that we can immediately write tests for them and leverage mocking to test for actual behaviors. This is a great advantage as it allows you to rapidly test to confirm your component is working without worrying about building or assembling objects in your tests. You have eliminated all kinds of crazy creation and assembler code and just concentrated yourself on the problem at hand. You are now focused to code the greatest piece of software you have ever imagined, thanks to WireBox!

So let's build our unit test \(Please note we use our base ColdBox testing classes for ease of use and [MockBox](http://wiki.coldbox.org/wiki/MockBox.cfm) integration\):

```javascript
component extends="coldbox.system.testing.BaseModelTest"{

    function setup(){
        // mock some owner
        mockOwner = getMockBox.createEmtpyMock("Owner");
        // create our coffee shop class with mocking capabilities
        shop = getMockBox().createMock("CoffeeShop").init(mockOwner);
        // mock the espresso machine
        mockMachine = getMockBox().createEmptyMock("EspressoMachine");
        // inject to the shop's variables scope to simulate DI
        shop.$property("espressoMachine","variables",mockMachine);
    }

    function testMakeEspresso(){
        // mock methods
        mockMachine.$("makeEspresso", createStub());
         // test
        shop.makeEspresso();
        assertTrue( mockMachine.$once('makeEspresso') );
    }

    function testOpenShop(){
        //mocks
        mockMachine.$("turnOn");
        mockOwner.$("nap");
        // test
        shop.openShop();
        assertTrue( mockMachine.$once('turnOn') );
        assertTrue( mockOwner.$once('nap') );
    }
}
```

Now we can run our tests and verify that our coffee shop is operational and producing sweet sweet espresso!


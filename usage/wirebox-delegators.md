---
description: Object Composition Elevated!
---

# WireBox Delegators

### What is Delegation?

WireBox supports the concept of [object delegation](https://en.wikipedia.org/wiki/Delegation\_\(object-oriented\_programming\)) in a simple, expressive DSL.&#x20;

Object delegation, also known as delegation design pattern, is a technique in object-oriented programming where one object delegates certain responsibilities to another object. Instead of inheriting behavior from a superclass (class inheritance), an object obtains behavior by delegating tasks to another object.&#x20;

WireBox provides a set of rules for method lookup and dispatching, allowing you to provide delegation easily in your CFML applications.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt="" width="563"><figcaption></figcaption></figure>

> This pattern is also known as "proxy chains". Several other design patterns use delegation - the State, Strategy and Visitor Patterns depend on it.

Let's discover some benefits of Delegators:

1. **Code Reusability:** Delegation promotes code reuse by allowing you to compose and reuse existing objects, enhancing modular design. You can create specialized delegate objects and reuse them in various contexts, avoiding the limitations of single inheritance.
2. **Separation of Concerns:** Delegation helps separate concerns and maintain a clear separation of responsibilities between objects. Each object focuses on its core functionality, and the delegated object handles specific tasks or services.
3. **Flexibility and Extensibility:** Delegation allows you to change behavior at runtime by switching delegate objects. You can introduce or modify new behavior without altering the main object's structure or functionality.
4. **Reduced Coupling:** Delegation reduces tight coupling between objects, leading to a more maintainable and loosely coupled codebase. Changes to the delegate object's implementation don't affect the main object, and vice versa.
5. **Better Composition:** Delegation supports a more flexible and fine-grained approach to combining behavior rather than class inheritance. You can compose objects with various delegate objects to achieve different combinations of features.
6. **Single Responsibility Principle (SRP):** Delegation aligns with the SRP, as each object focuses on a single responsibility. This promotes cleaner, more maintainable, and testable code.
7. **Encapsulation and Information Hiding:** Delegation allows encapsulation of internal behavior within the delegate object. The main object can provide a simplified interface, hiding complex implementation details.
8. **Dynamic Behavior:** Delegation facilitates dynamic behavior changes during runtime, making it suitable for scenarios where behavior needs to change based on different conditions or contexts.
9. **Easier Testing:** Delegation can lead to more focused and isolated unit tests. You can test delegate objects independently and mock them when testing the main object.
10. **Avoiding Fragile Base Class Problem:** Delegation helps avoid issues related to the fragile base class problem, which can occur when modifying superclass behavior affects subclasses.

It's important to note that while delegation offers these benefits, it might introduce some additional complexity to the codebase, especially when managing interactions between objects. Careful design and consideration are necessary to leverage delegation effectively.

### Why use Delegation?

In object-oriented programming, there are three ways for classes to work together:

1. [Inheritance](https://en.wikipedia.org/wiki/Inheritance\_\(object-oriented\_programming\)) (IS A relationship)
2. Composition (HAS A relationships)
3. Runtime Mixins or Traits

With [inheritance](https://stackify.com/oop-concept-inheritance/), you create families of objects or hierarchies where a parent component shares functions, properties, and instance data with any component that extends it (derived class). It’s a great way to provide reuse but also one of the most widely abused approaches to reuse. It’s easy and powerful but with much power comes great responsibility. For example, you create a base `Animal` class and then derived classes like: `Cat`, `Dog`, `Bird`, etc. You can say: A `Cat` **IS An** `Animal`, A `Dog` **IS An** `Animal`. You wouldn’t say, a `Cat` has an `Animal`.

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

With [composition](https://en.wikipedia.org/wiki/Object\_composition) a component will either create or have dependencies injected into them (via WireBox), which it can then use these objects to delegate work to them. This follows the `has a` relationship, like A Car has Wheels, a Computer has Memory, etc. The major premise of WireBox is to assist with composition.

Mixins allow you to do runtime injections of user-defined functions (UDFs) and helpers from reusable objects. However, this can lead to method explosion on injected classes, collisions, and not a lot of great organization as you are just packing a class with tons of functions to reuse behavior. Composition is the preferred approach and the less decoupled approach. Delegation is a step further. So let’s explore it with a simple example.

### Delegation by Example

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

A `Computer` is made from many parts, and each part does one thing really well. If you want to render something on the screen, the computer tells the graphics card and lets the card do its job. It tells it what to do but not **HOW** to do it. That’s **composition**. You wouldn’t want a computer to extend from a graphics card, or memory or a disk, right? You use them in orchestration. But what if you wanted to give the public access to the memory or graphics card? Or maybe log all calls to the memory module? You would have to build some bridge right, a proxy, a way to access those methods and delegate. So let’s explore how to do this manually:

**Memory**

```cfscript
component name="Memory"{

	function init(){
		return reset()
  }

	function reset(){
		variables.data = []
		return this;
  }

  function read( index ){
		return variables.data[ arguments.index ]
  }

  function write( data ){
	  variables.data.append( arguments.data )
  }

}

```

**Computer**

```cfscript
component name="computer"{

	// Inject a memory object via WireBox
  property name="memory" inject;

	// read delegator proxy method
  function read( index ){
		return variables.memory.read( argumentCollection = arguments )
  }

	// write delegator proxy method
  function write( data ){
		return variables.memory.read( argumentCollection = arguments )
  }

}

```

As you can see, we pass along the requests to the `Memory` object, and we satisfy our requirements. We can decorate these proxy methods if we want to as well to add behavior. However, imagine if you had many methods or many compositions and needed to do this for all those methods. As you can see, it can get very very tedious writing simple delegation methods. Here is where WireBox can assist.

{% hint style="success" %}
💡 WireBox Delegates are similar to object delegates in Kotlin, Groovy and Ruby, and Traits in PHP.
{% endhint %}

### A WireBox Delegate

You can annotate an injection with the `delegate` annotation and WireBox will inspect the delegate object for all its _public_ functions and create those functions at runtime for you in the target. This way, you don’t have to write all those delegation functions. Let’s look at our `Computer` again:f

```cfscript
component name="computer"{

	// Inject and use as a delegate
  property name="memory" inject delegate

}

computer = getInstance( "Computer" )
computer.read( index )
computer.write( data )
```

As you can see, the computer will magically have those `memory` delegation methods of `read() and write()` and will forward correctly to the `memory` module. This is great if you are using a full injection approach; not only do you get delegation but also a reference to the memory module via `variables.memory`.

### Component `Delegates` Annotation

However, we also have a shorthand annotation that you can use if you really don’t care about the injection but just about the delegations to happen. This is done by annotating your component with a `delegates` annotation.

```cfscript
component name="computer" delegates="Memory"{

   // code

}

computer = getInstance( "Computer" )
computer.read( index )
computer.write( data ) 
```

This annotation can be one or more delegates, and you can use either a WireBox ID or a full classpath:

```jsx
// Multiple Delegates by WireBox ID
component 
   name="computer" 
   delegates="Memory,FlowHelpers"{

   // code

}

// Delegates by Class Paths
component 
   name="computer" 
   delegates="models.system.Ram,
              models.util.FlowHelpers"{

   // code

}
```

{% hint style="danger" %}
**IMPORTANT** Please note that if you define multiple delegates and they have the same method names, the first defined delegate in the list will win unless you define specific prefixes or suffixes to distinguish the injections.
{% endhint %}

### Delegate Prefixes

If you need to prefix your delegate methods, then you can use the `delegatePrefix` annotation on your property injections. If you don’t give it a value, we will use the property's name as the prefix, or you can give it a value and be very explicit. Every method injected from the delegate will have that prefix.

```cfscript
component name="computer"

  property name="memory" inject delegate delegatePrefix
  property name="memory" inject delegate delegatePrefix="ram"

}

computer = getInstance( "Computer" )

// Implicit prefix
computer.memoryRead( index )
computer.memoryWrite( data )

// Explicit prefix
computer.ramRead( index )
computer.ramWrite( data )

```

This is great as you can be more expressive with the way those methods are delegated to.

#### Simple Shorthand Approach

But what about the simple delegate shortcuts approach? Does it support this? Yes, following the following pattern:

```jsx
delegates="[prefix>]WireBoxID|classPath"
```

This will allow you to add specific prefixes to distinguish the injections.

```cfscript
component name="computer" delegates="ram>Memory,FlowHelpers"{

   // code

}
```

The `Memory` object’s methods will be prefixed with `ram: ramRead(), ramWrite()`

You can also leave the prefix EMPTY, and we will use the object's name as the prefix.

```cfscript
component name="computer" delegates=">Memory,FlowHelpers"{

   // code

}
```

Since the `>Memory` is defined, then we will use `Memory` as the prefix.

### Delegate Suffixes

If you need to suffix your delegate methods, then you can use the `delegateSuffix` Annotation. If you don’t give it a value, we will use the property's name as the suffix or you can give it a value and be very explicit. Every method injected from the delegate will have that suffix.

```cfscript
component name="computer"

  property name="memory" inject delegate delegateSuffix
  property name="memory" inject delegate delegateSuffix="RAM"

}

computer = getInstance( "Computer" )
// Implicit
computer.readMemory( index )
computer.writeMemory( data )

// Explicit
computer.readRAM( index )
computer.writeRAM( data )

```

#### Simple Shorthand Approach

But what about the simple delegate shortcuts approach? Does it support suffixes? Yes, following the following pattern:

```jsx
delegates="[suffix<]WireBoxID|classPath"
```

This will allow you to add specific suffixes to distinguish the injections.

```cfscript
component name="computer" delegates="Ram<Memory,FlowHelpers"{

   // code

}
```

The `Memory` object’s methods will be suffixed with `ram: readRam(), writeRam()`

You can also leave the suffix EMPTY and we will use the name of the object as the suffix.

```cfscript
component name="computer" delegates="<Memory,FlowHelpers"{

   // code

}
```

Since the `>Memory` is defined, then we will use `Memory` as the suffix.

### Multiple Delegates

You can declare multiple delegates with no problem at all. All discovered public methods would be injected and delegated. However, if there is a case where each delegate has the same method name WireBox will throw a `DelegateMethodDuplicateException`. To avoid this side-effect, you will have to use suffixes or prefixes to remove the ambiguity.

```cfscript
component name="computer"

  property name="memory" inject delegate
  property name="disk" inject delegate

}

// Kaboom: DelegateMethodDuplicateException 
computer = getInstance( "Computer" )
// We can't even reach here.
computer.read( index )
computer.write( data )

```

To avoid conflicts, we recommend you use the suffixes and prefixes so the delegate methods are more expressive:

```cfscript
// Injection Approach
component name="computer"

  property name="memory" inject delegate delegatePrefix
  property name="disk" inject delegate delegateSuffix

}

// Shorthand Approach
component name="computer" delegates=">memory,<disk"

}

computer = getInstance( "Computer" )

// Using expressive delegation
computer.diskRead( index )
computer.writeMemory( data )

```

### Targeted Method Delegation

If you want to delegate to _only_ a few methods and not all public methods of an object, then you can use the `delegate` annotation and pass in a list of those methods you can to include in the delegation.

```cfscript
component name="computer"

  property name="memory" inject delegate delegatePrefix
  property name="disk" inject delegate="read,sleep" delegateSuffix
	property name="flow" inject="coldbox.system.util.core.Flow" delegate

}

computer = getInstance( "Computer" )
computer.diskRead()
computer.diskSleep()
computer.diskWrite() => Will FAIL!!!

```

#### Simple Shorthand Approach

The simple shorthand approach can also leverage targeted methods by adding the following pattern to the definition:

```jsx
delegates="[prefix|suffix><]WireBoxID|ClassPath[=methods]
```

You basically add the name of the methods by using a =`method` pattern.

```cfscript
component name="computer"
	delegates=">Memory, <Disk=read,sleep"
}

component name="computer"{

   property name="authorizable." 
		inject="provider:Authorizable@cbsecurity"
		delegate;

}
```

### Delegate $parent Injection

Every delegate, once it’s used on a target, will get a `$parent` injection available to them. This will allow them to interact with the parent that called for the delegation.

> **Important:** Please note that if your Delegate is a singleton, this can cause issues as it can be potentially injected into many parents. Therefore, we suggest that if you create Delegates that use the `$parent` approach, they remain as transients.

```cfscript
component{

	function populate( memento ){
		// Populate the injected parent
	       return populateFromStruct( target : $parent, memento : arguments.memento );
	}

}
```

### Binder Delegates Support

You can also explicitly set the `delegates` shorthand expression for a component via the binder’s `delegates()` method.

```jsx
map( "Computer" )
	.to( "path.Computer" )
	.delegates( ">Memory, <Disk(read,sleep)" )
	.delegates( [ ">Memory", "" ] )
```

You can also use the `property` binder method as well to explicitly define the delegate annotations of any injection property:

```jsx
/**
 * Map property injection
 *
 * @name             The name of the property to inject
 * @ref              The reference mapping id this property maps to
 * @dsl              The construction dsl this property references. If used, the name value must be used.
 * @value            The explicit value of the property, if passed.
 * @javaCast         The type of javaCast() to use on the value of the value. Only used if using dsl or ref arguments
 * @scope            The scope in the CFC to inject the property to. By default it will inject it to the variables scope
 * @required         If the property is required or not, by default we assume required DI
 * @type             The type of the property
 * @delegate         If the property is an object delegate it will be empty or the list of methods to delegate to, else null
 * @delegatePrefix   If the property has a delegate prefix, else null
 * @delegateSuffix   If the property has a delegate suffix, else null
 * @delegateExcludes If the property has a delegate exclusion list, else null
 * @delegateIncludes 
 */
Binder function property(
	required name,
	ref,
	dsl,
	value,
	javaCast,
	scope            = "variables",
	required required=true,
	type             = "any",
	delegate,
	delegatePrefix,
	delegateSuffix,
	delegateExcludes=[],
  delegateIncludes=[]
)
```

### Core Delegates

Now that we have seen what delegators are, WireBox offers core delegators to your application via the `@coreDelegates` namespace

* **Async** - This delegate is useful to interact with the AsyncManager and is the most used functionality for asynchronous programming.
* **DateTime** - Leverage the date time helper
* **Env** - Talk to environment variables
* **Flow** - Several fluent flow methods
* **JsonUtil** - JSON utilities
* **StringUtil** - String utilities
* **Population** - Population utilities

{% embed url="https://s3.amazonaws.com/apidocs.ortussolutions.com/coldbox/7.0.0/coldbox/system/core/delegates/package-summary.html" %}
API Docs
{% endembed %}

So let's say you have a service that needs to populate objects and work with the system environment:

```javascript
component 
    delegates="population@coreDelegates, Env@coreDelegates"{
}
```

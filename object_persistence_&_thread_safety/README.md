# Object Persistence & Thread Safety

While the injector can help in many ways to secure the creation of your objects, it is ultimately up to you to create code that is both thread safe and tested. It is always a great idea to design your objects without the injector in mind for threading and concurrency. 

DI is not a silver bullet, but a tool to relieve object creation and not to relieve the burden of good object design. Thread safety is much more complex and can be compromised when using persistent scopes like singleton, session, server, application and cachebox, as more than one thread will be trying to access your code and dependencies. 

The only guarantee the injector can provide is the constructor and constructor dependency creation to be completely locked. The following object is to be guaranteed to be locked when created and wired with dependencies:

```javascript
component{

     /**
     * @log.inject logbox:logger:{this}
     * @dao.inject id:MyDAO
     */
     function init(required log, required dao){
          variables.log = arguments.log;
          variables.dao = arguments.dao;
          return this;
     }

}
```

<br>

> **Important** The inject annotations are done in comments as ColdFusion 9 has a bug when adding annotations on scripted arguments. 

<br>

An example of a flawed object could be the following:

```javascript
component{

     property name="dao" inject="id:MyDAO";
     property name="log" inject="logbox:logger:{this}";

     function init(){
          return this;
     }
}
```

Why is this object flawed? It is flawed because the majority of DI engines, including WireBox, will lock for constructing the object and its constructor arguments. However, once it is constructed, it will store the object in the persistence scope of choice in order to satisfy the potential of circular dependencies in the object graph. After it is placed in the storage, the DI engines will wire up setter and property mixin injections and WireBox's `onDiComplete()` method. With this normal approach, the wiring of dependencies and `onDiComplete()` have the potential of mixups or missing dependencies due to concurrency. This is a normal side-effect and risk that developers take due that Java makes no guarantees that any thread other than the one that set its dependencies will see the dependencies. The memory between threads is not final or immutable so properties can enter an altered state.

>"The subtle reason has to do with the way Java Virtual Machines (JVM) are designed to manage threads. Threads may keep local, cached copies of non-volatile fields that can quickly get out of sync with one another unless they are synchronized correctly."
<br><small>From Dependency Injection by Dhanji R. Prasanna</small>

<br>

> **Note** This side effect of concurrency will only occur on objects that are singletons or persisted in scopes like session, server, application, server or cachebox. It does not affect transient or request scoped objects. 

WireBox, can help you lock and provide thread safety to setter and property injections by providing you with the `ThreadSafe` annotation or our binder `threadSafe()` tagging method. So if we wanted to make the last example thread safe for property and setter wiring then we would do the following:

```javascript
component threadSafe{

     property name="dao" inject="id:MyDAO";
     property name="log" inject="logbox:logger:{this}";

     function init(){
          return this;
     }
}

// or
component threadSafe=true{

     property name="dao" inject="id:MyDAO";
     property name="log" inject="logbox:logger:{this}";

     function init(){
          return this;
     }
}

// or you can bind it as a thread safe component
map("MyObject").to("path.model.MyObject").asSingleton().threadSafe();
```

> **Note** All objects are marked as non thread safe for dependency wiring by default in order to allow for circular dependencies. Please note that if you mark an object as threadSafe, then it will not be able to support circular dependencies unless it uses WireBox providers. ( See Providers Section )  

<br>

Our threadSafe annotation and binder tagging property will allow for these objects to be completely locked and synchronized for object creation, wiring and onDiComplete(). However, circular dependencies will now fail as persistence cannot be guaranteed for the setter or property dependencies. However, since WireBox is so awesome, you can still use circular dependencies by wiring instead our object providers. (Please see providers section). In conclusion, constructing and designing a CFC that is thread safe is often a very arduous process. It is also very difficult to test and recreate threading issues in your objects and applications. So don't feel bad, as even the best of us can get into some nasty wormholes when dealing with concurrency and thread safety. However, always try to design for as much concurrency as possible and test test test!


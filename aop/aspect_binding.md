# Aspect Binding

Since we have now mapped our aspect in WireBox, we now need to tell it the most important things:


1. To what classes or CFCs should we apply this aspect to?
2. To what methods or join points should we apply this aspect to?

We do this with another binder DSL method:

* bindAspect(classes,methods,aspects)

```javascript
bindAspect(classes=match().mappings('UserService'),methods=match().methods('save'),aspects="MethodLogger");
```

What is up with that funky match().... stuff? Well, the classes and methods arguments of the bindAspect() call uses our AOP funky matcher methods that exist in an object called: coldbox.system.aop.Matcher. This matcher object is used to match classes and methods to whatever criteria you like. The binder has a convenience method called match() that creates a new matcher object for you and returns it so you can configure it for classes and method matching. Here are the most common matching methods below:

|Method|Class Matching|Method Matching|Description|
|--|--|--|--|
|any()|true|true|Matches against any class path or method name|
|returns(type) |false |true |Matches against the return type of methods|
|annotatedWith(annotation,[value]) |true |true |Matches against the finding of an annotation in a cfcomponent or cffuntion or matches against the finding AND value of the annotation.|
|mappings(mappings) |true |false |Matches to ONLY the named mapping(s) you pass to this method as a list or array.|
|instanceOf(classPath) |true |false |Matches if the target object is an instance of the classPath. This internally uses the ColdFusion isInstanceOf() method|
|regex(regex) |true|true |Matches against a CFC instantiation path or function name using regular expressions|
|methods(methods) |false |true |Matches against a list of explicit method names as a list or array|
|andMatch(matcher) |true |true |Does an AND evaluation with the current matcher and the one you pass in the method.|
|orMatch(matcher) |true |true |Does an OR evaluation with the current matcher and the one you pass in the method.|

WOW! We can really pin point anything in our system! So now that we have binded our aspect to our UserService I can rewrite it to this:

```javascript
component name="UserService"{

	function save(){

	  transaction {
	     // do some work here
	  }

	}
}
```

Now isn't that pretty? Much nicer and compact hugh! Plus I can reuse the method logger for ANY method in ANY class I desire (Muaaaahaaaa), that's an evil laugh by the way! But we are not done, let's keep going and do the Transactional aspect.

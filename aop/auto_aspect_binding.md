# Auto Aspect Binding
WireBox AOP supports the concept of self aspect bindings. This means that we can make things even simpler by letting the Aspect you build control what class and methods it will match against. This is great, one less thing to remember when developing the code. So let's start with the code first:

```javascript
/**
* @classMatcher any
* @methodMatcher annotatedWith:transactional
*/
component name="TransactionAspect" implements="coldbox.system.aop.MethodInterceptor"{

	function init(){ return this; }

	function invokeMethod(required invocation) output=false{

		// Let's do the around advice now:
		transaction {
			// execute the method or other aspects in a transaction
			return arguments.invocation.proceed();
		}

	}
}
```
That's it! Our transaction aspect is done and it will also bind itself to ANY class and ANY method that has the transactional annotation. Then you just map it:

```javascript
mapAspect("TransactionAspect").to("model.aspects.MyTransactionAspect");
```
We are done now, by mapping the aspect WireBox detects the two annotations classMatcher and methodMatcher and binds it for you. WOW, but where did you get that from? Well, the component has two annotations:

```javascript
/**
* @classMatcher any
* @methodMatcher annotatedWith:transactional
*/
OR
component classMatcher="any" methodMatcher="annotatedWith:transactional"{}
```

How cool is that! My aspect can determine the matching for me already. So what can I use for these matchers:

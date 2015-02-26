# Summary

So now that we mapped our self binding aspect, let's clean up our code further:

```javascript
component name="UserService"{

	function save() transactional{
		// do some work here
	}
}
```

Now isn't this amazing! We are back to our original business logic and code with no extra fluff around logging, transactions and pretty much just code noise. Now we are talking and cooking with AOP. So hopefully by now you nave a good grasp of what AOP does for you and how to implement it in WireBox. So here are the steps to remind you:


* Create an aspect that implements: coldbox.system.aop.MethodInterceptor
* Map the aspect in your WireBox binder
* Bind the aspect to classes and methods

So, easy as 1-2-3! AOP is powerful and extermely flexible. Hopefully, your imagination is now going into overdrive and coming up with ways to not only clean up your code from cross cutting concerns, but also help you do things like:


* threaded methods
* transform method results
* method auditing
* method security
* cache method results
* etc.

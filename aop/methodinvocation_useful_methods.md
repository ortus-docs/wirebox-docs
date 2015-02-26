# MethodInvocation Useful Methods

Here are a list of the most useful methods in this CFC

* getMethod() : Get the name of the method (join point) that we are proxying and is being executed
* getMethodMetadata() : Get the metadata structure of the current executing method. A great way to check for annotations on the method (join point)
* getArgs() : Get the argument collection of the method call
* setArgs() : Override the argument collection of the method call
* getTarget() : Get the object reference to the target object
* getTargetName() : Get the name of the target object
* getTargetMapping() : Get the object mapping of the proxied object.
* Great for getting metadata information about the object, extra attributes, etc.
* proceed() : This is where the magic happens, this method tells WireBox AOP to continue to execute the target method. If you do not call this in your aspect, then the proxyied method will NOT be executed.


The last method is the most important one as it tells WireBox AOP to continue executing either more aspects, the proxyed method or nothing at all.

<img src="../images/WireBoxAOP-MethodProceed.jpg">

# WireBox Listeners

We have already seen in our previous section all the events that are announced by WireBox, but how do we listen? 

There are two ways to build WireBox listeners because there are two modes of operations, but the core is the same. Listeners are simple CFCs that must create methods that match the same name of the event they want to listen to. If you are running WireBox within a ColdBox application, listeners are [Interceptors](http://wiki.coldbox.org/wiki/Interceptor.cfm) and you declare them and register them exactly the same way that you do with normal interceptors. Also, these methods can take up to two parameters depending on your mode of operation (standalone or coldbox). The one main difference between pure Wirebox listeners and ColdBox interceptors are that the configure method for the standalone WireBox is different. Please see samples.

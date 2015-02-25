# Providers

Let's get funky now! We have seen how to inject objects and how to scope objects. However, we need to talk about a cool WireBox feature called object providers. We learned that when you request an object from WireBox it creates it and injects it immediately. However, sometimes we need more control like:

* Delay construction of the dependency until some point in time during your controlled execution. Maybe you don't want to construct some dependencies until some feature in your application is enabled.
* You need multiple instances of a class. Like a User service producing transient users, or our espresso machine creating espressos.
* You need to access scoped objects that might need reconstruction. Maybe you want to check the cache first for existence or a ColdFusion scope in order to avoid scope widening injection.
* You have some old legacy funkiness for building stuff that has to remain as its own factory

All of these areas is where WireBox Providers can really save the day. WireBox offers automatically a way to create providers for you by creating generic provider classes (coldbox.system.ioc.Provider) that will be configured to provide the mapping you want, then injected instead of the real object requested. This happens whenever you use the provider DSL injection namespace or annotate methods with a provider annotation. It also gives you an interface (coldbox.system.ioc.IProvider), which is very simple, that you can implement in order to register your own complex providers with WireBox. You would usually do the latter if you have legacy code you need to abstract out, had funky construction processes, etc. Let's start by looking at how registering custom providers work first and then how to use the automatic WireBox providers work.

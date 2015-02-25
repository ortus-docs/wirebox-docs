# Features at a Glance

Here are a simple listing of features WireBox brings to the table:

* Annotation driven dependency injection
* 0 configuration mode or a programmatic binder configuration approach via ColdFusion (No XML!)
* Creation and Wiring of or by:
 * ColdFusion Components
 * Java Classes
 * RSS Feeds
 * WebService objects
 * Constant values
 * DSL string building
 * Factory Methods
* Multiple Injection Styles: Property, Setter, Method, Constructor
* Automatic Package/Directory object scanning and registration
* Multiple object life cycle persistence scopes:
 * No Scope (Transients)
 * Singletons
 * Request Scoped
 * Session Scoped
 * Application Scoped
 * Server Scoped
 * CacheBox Scoped
* Integrated logging via [LogBox](http://logbox.ortusbooks.com), never try to figure out what in the world the DI engine is doing
* Parent Factories
* Factory Method Object Creations
* Object life cycle events via WireBox Listeners/Interceptors
* Customizable injection DSL
* WireBox object providers to avoid scope-widening issues on time/volatile persisted objects
* [Aspect Oriented Programming](../aop/index.md)
* [Standalone ORM Entity Injection](orm_entity_injection/README.md)

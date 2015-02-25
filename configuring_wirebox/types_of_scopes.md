# Types of Scopes
Each configuration binder has two public properties accessible in the this scope:

1. this.TYPES : A reference to coldbox.system.ioc.Types used to declare what type of object you are registering for construction or wiring
2. this.SCOPES : A reference to coldbox.system.ioc.Scopes used to declare in what life cycle scope the object will be stored under

These two classes contain static public members in the this scope that facilitate the declaration of persistence scopes and construction types for object mappings. Below are the valid enumerations for these two classes:

<h4 style="color:blue">this.TYPES</h4>

* CFC : Construction of a CFC
* JAVA : Construction of a Java class
* WEBSERVICE : Construction of a webservice object
* RSS : Construction of an RSS feed
* DSL : Construction by DSL string
* CONSTANT : A constant value
* FACTORY : Construction by factory method


<h4 style="color:blue">this.SCOPES</h4>
* NOSCOPE : Transient objects
* PROTOTYPE : Transient objects
* SINGLETON : Objects constructed only once and stored in the injector
* SESSION : ColdFusion session scoped based objects
* APPLICATION : ColdFusion application scope based objects
* REQUEST : ColdFusion request scope based objects
* SERVER : ColdFusion server scope based objects
* CACHEBOX : CacheBox scoped objects

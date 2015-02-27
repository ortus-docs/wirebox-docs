# Custom Providers
If you need to abstract old legacy code or have funky construction processes, we would recommend you build your own provider objects. This means that you will create a component that implements `wirebox.system.ioc.IProvider` (one `get()` method) and then you can map it. Once mapped, you can use it anywhere WireBox listens for providers:

* The Injection DSL &rarr;

```javascript
property name="" inject="provider:{name or injectionDSL}";
```

* The mapping DSL

```javascript
map("MyCFC").toProvider('name or injectionDSL')

// or
setter,property,methodArg,initArg(name="",dsl="provider:{name or injectionDSL}");
```
<br>
Here is the interface you need to implement:
```javascript
<cfinterface hint="The WireBox Provider Interface that follows the provider pattern">
	<---  get --->
    <cffunction name="get" output="false" access="public" returntype="any" hint="Get the provided object">
    </cffunction>
</cfinterface>
```
<br>

The CFC you build will need to be mapped so it can be retrieved by name and also so if it needs DI or any other WireBox funkiness, it can get it. So let's look at our FunkyEspressoProvider that we needed to create since we have some old legacy machines that we need to revamp:

```javascript
component name="FunkyEspressoProvider" implements="coldbox.system.ioc.IProvider" singleton{

	property name="log" inject="logbox:logger:FunkyEspressoProvider";

	public function init(){ return this; }

	Espresso public function get(){
		// log
		log.canDebug(){ log.debug("Requested funky espresso"); }
		var espresso = createObject("component","old.legacy.Espresso").init();
		// add some sugar as the old legacy machine is not that great.
		espresso.addSugar(1);
		// returned provided object.
		return espresso;
	}

}
```
<br>
Finally we map to the provider using the `.toProvider()` mapping method in the binder so anytime somebody requests an Espresso we can get it from our funky provider. Please note that I also map the provider because it also has some DI needed.

```javascript
component extends="coldbox.system.ioc.config.Binder"{
	function configure(){
		// map the provider first, so it can be constructed and DI performed on it.
		map("FunkyEspressoProvider")
			.to("model.legacy.FunkyEspressoProvider");

		// map espresso's to the old funky provider for construction and retrieval.
		map("Espresso")
			.toProvider("FunkyEspressoProvider");

	}
}
```
<br>
Cool! That's it, anytime you request an Espresso, WireBox will direct its construction to the provider you registered it with.

# WireBox Injector Interface

We also provide an interface to create objects that adhere to our injector interface: `wirebox.system.ioc.IInjector`. Then these objects can be used as parent injectors, which are great for legacy factories or creating hierarchies according to your specs. All you have to do is implement the following interface:

```javascript
<cfinterface hint="An interface that enables any CFC to act like a parent injector within WireBox">

	<---  setParent --->
    <cffunction name="setParent" output="false" access="public" returntype="void" hint="Link a parent Injector with this injector">
    	<cfargument name="injector" required="true" hint="A WireBox Injector to assign as a parent to this Injector">
    </cffunction>

	<---  getParent --->
    <cffunction name="getParent" output="false" access="public" returntype="any" hint="Get a reference to the parent injector instance, else an empty simple string meaning nothing is set" >
    </cffunction>

	<---  getInstance --->
    <cffunction name="getInstance" output="false" access="public" returntype="any" hint="Locates, Creates, Injects and Configures an object model instance">
    	<cfargument name="name" required="false" 	hint="The mapping name or CFC instance path to try to build up"/>
		<cfargument name="dsl"	required="false" 	hint="The dsl string to use to retrieve the instance model object, mutually exclusive with 'name'"/>
		<cfargument name="initArguments" required="false" 	hint="The constructor structure of arguments to passthrough when initializing the instance"/>
	</cffunction>

	<---  containsInstance --->
    <cffunction name="containsInstance" output="false" access="public" returntype="any" hint="Checks if this injector can locate a model instance or not">
    	<cfargument name="name" required="true" hint="The object name or alias to search for if this container can locate it or has knowledge of it"/>
    </cffunction>

	<---  shutdown --->
    <cffunction name="shutdown" output="false" access="public" returntype="void" hint="Shutdown the injector gracefully by calling the shutdown events internally.">
    </cffunction>

</cfinterface>
```

<img src="../images/injectorInterface_hierarchies.jpg">

Once you create this CFC that implements this interface then you can call on the injector's setParent() method and you are ready to roll.

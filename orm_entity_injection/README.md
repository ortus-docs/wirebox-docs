# ORM Entity Injection
WireBox 2.0.0 supports entity injection via

* [ColdBox ORM Module](https://github.com/coldbox/cbox-cborm) - for use in ColdBox applications
* **Custom ORM Event Handler** - for use in any CFML application

## Custom ORM Event Handler

In order to leverage WireBox for entity injection you will have to create your own custom ORM event handler and activate event handling in the ORM at the `Application.cfc`

```js
this.ormSettings = {
	cfclocation="model",
	dbcreate = "update",
	dialect = "MySQLwithInnoDB",
	logSQL = true,
	// Enable event handling
	eventhandling = true,
	// Set the event handler to use, which will be inside our application or the default wirebox one
	eventhandler = "model.ORMEventHandler"
};
```

Then you can create the custom event handler with a custom `postLoad()` function where you will leverage WireBox for DI.

```js
component implements="CFIDE.orm.IEventHandler"{
    
    /**
	* postLoad called by hibernate which in turn announces a coldbox interception: ORMPostLoad
	*/
	public void function postLoad(any entity){
		application.wirebox.autowire( 
		    target=arguments.entity, 
		    targetID="ORMEntity-#getMetadata( arguments.entity ).name#" 
		);
	}

}


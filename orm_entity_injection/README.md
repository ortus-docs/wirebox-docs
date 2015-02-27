# ORM Entity Injection
WireBox 2.0.0 supports entity injection via

* [ColdBox ORM Module](https://github.com/coldbox/cbox-cborm) - for use in ColdBox applications
* Custom ORM Event Handler - for use in any CFML application

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




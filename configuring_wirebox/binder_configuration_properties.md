# Binder Configuration Properties

Whether you use WireBox standalone or within a ColdBox context a Binder gets a structure of configuration properties so it can use them whenever you are configuring it or declaring mappings. If you are in standalone mode, the Injector can be constructed with a properties structure that will be passed to the binder for usage. If you are in a ColdBox application the ColdBox application configuration structure is passed for you. You can then use these properties with the following methods:

* getProperty(name,[default]) : Get a specific property
* getProperties() : Get all the properties structure
* propertyExists(name) : Check if a property exists
* setProperty(name,value) : Dynamically add properties to the structure


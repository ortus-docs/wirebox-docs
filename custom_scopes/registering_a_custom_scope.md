# Registering a Custom Scope

```javascript
customScopes = {
	ortus = "path.model.dsl.OrtusScope"
};

or
mapScope("ortus","path.model.dsl.OrtusScope");

```

Now I can use the ortus scope in my mappings DSL and even my annotations, isn't that cool!

```javascript
component scope="ortus"{

}

// map it
map("Luis")
	.to("model.path.LuisService")
	.into("Ortus");
```

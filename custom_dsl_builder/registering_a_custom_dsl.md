# Registering a Custom DSL

```javascript
customDSL = {
	ortus = "path.model.dsl.MyDSL"
};

or
mapDSL("ortus","path.model.dsl.MyDSL");

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

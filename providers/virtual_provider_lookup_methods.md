# Virtual Provider Lookup Methods

This is a feature where you can mark methods in your components with a special `provider` annotation so they can serve the objects you requested automatically for you. This is an amazing feature as it will take the original method signature and replace the method for you with one that will serve the provided objects for you automatically. How insane is that! You deserve some <b>getting jiggy wit it (chapter 4) </b> dancing!

```javascript
public Espresso function getEspresso() provider="espresso"{}
```

Wow! That's it! Yep, just create an empty method signature and annotated with `provider={mapping}` and then WireBox will read these annotated methods and replace them for you at runtime so when you call `etEspresso()` it actually calls the WireBox injector and requests a new espresso instance and it returns it.

> **Important** Please note that the visibility of provided methods does not matter to WireBox. It can provide `public, private, or packaged` visibilities with no problem at all.
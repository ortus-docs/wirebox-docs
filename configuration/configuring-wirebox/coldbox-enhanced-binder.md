# ColdBox Enhanced Binder

If you are using your configuration binder within a ColdBox application you will have some extra goodies in the Binder that come in very handy:

* `getColdBox()` : Retrieve the instance of the running ColdBox application
* `getAppMapping()` : Get the current `AppMapping`, the location of the application on th server, setting for the running ColdBox application

```javascript
// map the model folder
mapDirectory( getAppMapping() & ".model" );
```

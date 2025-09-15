# Processing Mappings

Since version 5.5.0 all mappings in WireBox will **only** be processed when they are requested for the very first time.  This is to enhance performance and increase startup times.  Processing means that the object's and its inheritance trail are inspected for metadata, which can be a very time consuming process.

### process()

However, you can explicitly process a mapping right after mapping it via the binder's `process()` method.

```javascript
mapPath( "com.app.Service" ).process();
```

That's it! If you call the `process()` method right after a mapping, it will be automatically processed.  This means all annotations will be inspected.

### mapDirectory( process=true )

If you are mapping using mapDirectory() then you can pass the `process` argument to true and all mappings in that directory scan will be processed automatically.

```javascript
mapDirectory( packagePath="models.services", process=true );
// or
mapDirectory( "models.services" ).process();
```


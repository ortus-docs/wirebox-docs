# MethodLogger

This aspect enables you to log method calls and their results. You will have to bind it to the methods you want it to listen to. It has one constructor argument:

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| logResults | boolean | false | true | Whether to log the results of method calls or not. |

```javascript
// Map the Aspect
mapAspect("MethodLogger")
    .to("coldbox.system.aop.aspects.MethodLogger")
    .initArg(name="logResults",value="true or false");

// Bind the Aspect to all service class methods
bindAspect(classes=matcher().regex('.*Service'), methods=matcher().any(), aspects="MethodLogger");
```


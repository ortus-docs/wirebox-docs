# MethodMatcher Annotation DSL
Create a `methodMatcher` annotation on the component with the following DSL values:

|DSL|Description|
|--|--|
|any|Matches against any class path or method name|
|annotatedWith:{annotation} |Matches against the finding of an annotation in a cfcomponent|
|annotatedWith:{annotation}:{value} |Matches against the finding of an annotation value in a cfcomponent|
|returns:{type} |Matches to ONLY the methods that return the {type}|
|methods:{methods} |Matches to ONLY the named methods(s) you pass to this method as a list or array.|
|regex:{regex} |Matches against a CFC instantiation path or function name using regular expressions|

## Overiding Bindings
One thing to note about self binding aspects is that you can also override their matching by using the `autoBind` argument in the `mapAspect()` method call. So if you wanted to override the class and method matching on this aspect you would do this:

```javascript
mapAspect(aspect="TransactionAspect",autoBind=false).to("model.aspects.MyTransactionAspect");

// match only methods that start with the regex ^save
bindAspect(classes=match().any(),methods=match().regex("^save"),aspects="TransactionAspect");
```


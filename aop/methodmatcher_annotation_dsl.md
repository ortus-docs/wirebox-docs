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




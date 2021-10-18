# ClassMatcher Annotation DSL

Create a `classMatcher` annotation on the component with the following DSL values:

| DSL                                | Description                                                                                                              |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| any                                | Matches against any class path or method name                                                                            |
| annotatedWith:{annotation}         | Matches against the finding of an annotation in a cfcomponent                                                            |
| annotatedWith:{annotation}:{value} | Matches against the finding of an annotation value in a cfcomponent                                                      |
| mappings:{mappings}                | Matches to ONLY the named mapping(s) you pass to this method as a list or array.                                         |
| instanceOf:{classPath}             | Matches if the target object is an instance of the classPath. This internally uses the ColdFusion isInstanceOf() method. |
| regex:{regex}                      | Matches against a CFC instantiation path or function name using regular expressions                                      |

# What's New With 5.0.0

This release is part of the ColdBox 5.0.0 upgrade and it is a major release.  Below you will find the major areas of improvement for WireBox and the full release notes.

## Error Reporting

We have done greats strides in consistency of error reporting during the creation of objects and their wiring.  We have also added countermeasures for **rogue** mappings that could bring entire applications down.  You will now get more consistency and better error reporting overall.

## AOP Performance

AOP now performs in over 70% faster than previous implementations.  In previous versions, we would create intermediate class files that would then be loaded and injected as part of the AOP proxies.  This took time and not only that, it would create 1 stub per call to a method implementation.  Our strategy worked but lacked performance.  In 5.0.0 we completely re-architected the way we did method injection and stub creation.  We now take md5 hashes of the source code to be injected and only created the stubs 1 per-lifetime.  The improvements are drastic and amazing.  Enjoy AOP and don't hold back! 

## DI Performance

We have moved from an `instance` scope approach to a `variables` scope approach with accessors and mutators in 5.0.0 and yet again we benefit from CFML engine speed improvements.  Again, thanks to the community for many pull requests.


## Release Notes
            
### Bugs

* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-29'>WIREBOX-29</a>] - Virtual inheritance breaks AOP on on base class methods.
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-52'>WIREBOX-52</a>] - Virtual Inheritance doesn&#39;t inherit variables-scoped properties
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-63'>WIREBOX-63</a>] - CFC&#39;s with same name don&#39;t get aliases picked up with mapDirectory()
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-64'>WIREBOX-64</a>] - Illusive double id exception when race conditions
            
### New Features


* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-58'>WIREBOX-58</a>] - Allow new listeners added to the Binder to also be registered right away, especially from modules
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-62'>WIREBOX-62</a>] - New request context dsl injection -&gt; coldbox:requestContext
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-67'>WIREBOX-67</a>] - New coldbox dsl element =&gt; coldbox:router to retrieve the application&#39;s router object.
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-68'>WIREBOX-68</a>] - Virtual Inheritance now copies over properties and private functions with generic accessors
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-69'>WIREBOX-69</a>] - Module Injection Shortcut when the inject annotation is @moduleAdress
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-70'>WIREBOX-70</a>] - Add a new `onLoad()` method interceptor for WireBox configuration binder
        
### Improvements

* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-28'>WIREBOX-28</a>] - Improve errors while building depenencies
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-34'>WIREBOX-34</a>] - Improve AOP binding by caching temp files
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-59'>WIREBOX-59</a>] - Throw error on non-existent coldbox DSL
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-65'>WIREBOX-65</a>] - Increase Wirebox performance by scoping variables
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-66'>WIREBOX-66</a>] - Complete refactoring of wirebox scopes/DSL to script and direct scope usage
* [<a href='https://ortussolutions.atlassian.net/browse/WIREBOX-71'>WIREBOX-71</a>] - Ability to cache metadata in CacheBox 
                                        
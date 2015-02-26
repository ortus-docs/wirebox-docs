# Overview

> Dependency injection is the art of making work come home to you.<br>
> <small> <i>Dhanji R. Prasanna</i></small>


<img src="../images/overview_WireBoxIcon.png" width="46%" style="float:left">

<p>WireBox alleviates the need for custom object factories or manual object creation in your ColdFusion applications. It provides a standardized approach to object construction and assembling that will make your code easier to adapt to changes, easier to test, [mock](http://wiki.coldbox.org/wiki/MockBox.cfm) and extend.</p>

<p>As software developers we are always challenged with maintenance and one ever occurring annoyance,change. Therefore, the more sustainable and maintainable our software, the more we can concentrate on real problems and make our lives more productive. WireBox leverages an array of metadata annotations to make your object assembling, storage and creation easy as pie! We have leveraged the power of event driven architecture via object listeners or interceptors so you can extend not only WireBox but the way objects are analyzed, created, wired and much more. To the extent that our [AOP](http://wiki.coldbox.org/wiki/WireBox-AOP.cfm) capabilities are all driven by our AOP listener which decouples itself from WireBox code and makes it extremely flexible.</p>

<p>We have also seen the value of a central location for object configuration and behavior so we created our very own WireBox Programmatic Mapping DSL ([Domain Specific Language](http://en.wikipedia.org/wiki/Domain-specific_language)) that you can use to define object construction, relationships, AOP, etc in pure ColdFusion (No XML!). We welcome you to stick around and read our documentation so you can see the true value of WireBox in your web applications.</p>

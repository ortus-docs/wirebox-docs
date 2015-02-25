# Dependencies DSL

The dependencies DSL methods are mostly used to define dependencies and also to activate advanced features on target objects, such as runtime mixins, virtual inheritance, etc.

<br>
<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="10%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Please note that you can concatenate more than one of these methods calls to dictate multiple constructor arguments, setter methods, cf properties, and more. </b></p>
<div style="clear:both"></div>
</div>
<br>

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Method Signature</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>constructor</b>(constructor) </td>
<td>Tells WireBox which constructor to call on the mapped object. By default if an object has an <i>init()</i> method, that will be used as the constructor</td></tr>
<tr>
<td><b>noInit()</b> </td>
<td>Tells WireBox that this mapped object will skip the constructor call for it. By default WireBox always calls object constructors</td></tr>
<tr>
<td><b>threadSafe()</b> </td>
<td>Tells WireBox that the mapped object should be constructed and then wired with a strict concurrency lock for property injections, setter injections and onDIComplete(). Please be aware that if you use this mode of construction, circular dependencies are not allowed. The default is that property and setter injections and onDIComplete() are outside of the construction locks.</td></tr>
<tr>
<td><b>notThreadSafe()</b> </td>
<td>Tells WireBox to construct objects by locking only the constructor and constructor argument dependencies to allow for circular dependencies. This is the default construction mode of all persisted objects: singleton, session, server, application and cachebox scope.</td></tr>
<tr>
<td><b>noAutowire()</b> </td>
<td>Tells WireBox that this mapped object has its dependencies described programmatically instead of using metadata inspection to discover them.</td></tr>
<tr>
<td><b>parent(alias)</b> </td>
<td>Tells WireBox that this mapped object has a parent mapping with definitions it should use to base it from. This feature provides a great way to reuse object mapping definitions.</td></tr>
<tr>
<td><b>initArg</b>([name],[ref],[dsl],[value],[javaCast]) </td>
<td>Used to define a constructor argument for the mapped object.
<ul>
<li><b>name</b> : The name of the constructor argument. Not used for Java or Webservice construction</li>
<li><b>ref</b> : The mapping reference id this constructor is mapped to. E.G. ref='MyFunkyEspresso'</li>
<li><b>dsl</b> : The construction dsl that will be used to construct this constructor argument</li>
<li><b>value</b> : The constant value you can use instead of a dsl or ref for this constructor argument</li>
<li><b>javaCast</b> : If using a java object, you can cast the value of this constructor argument</li></ul></td></tr>
<tr>
<td><b>initWith()</b> </td>
<td>You can pass as many arguments (named or positional) to this method to simulate the <i>init()</i> call of the mapped object. WireBox will then use that argument collection to initialize the mapped object. Note, <i>initWith()</i> only accepts arguments which can be evaluated at the time the binder is parsed such as static values, or binder properties. To specify mapping IDs or DSLs, use <i>initArg()</i>.</td></tr>
<tr>
<td><b>methodArg</b>([name],[ref],[dsl],[value],[javaCast]) </td>
<td>Used to define a factory method argument for the mapped object when using a factory method construction.
<ul>
<li><b>name</b> : The name of the method argument. Not used for Java or Webservice construction</li>
<li><b>ref</b> : The mapping reference id this method argument is mapped to. E.G. ref='MyFunkyEspresso'</li>
<li><b>dsl</b> : The construction dsl that will be used to construct this method argument</li>
<li><b>value</b> : The constant value you can use instead of a dsl or ref for this method argument</li>
<li><b>javaCast</b> : If using a java object, you can cast the value of this method argument</li></ul></td></tr>
<tr>
<td><b>property</b>([name],[ref],[dsl],[value],[javaCast],[scope]) </td>
<td>Used to define a property mixin that will occur at runtime.
<ul>
<li><b>name</b> : The name of the property value to inject. Not used for Java or Webservice construction</li>
<li><b>ref</b> : The mapping reference id this property is mapped to. E.G. ref='MyFunkyEspresso'</li>
<li><b>dsl</b> : The construction dsl that will be used to construct this property argument</li>
<li><b>value</b> : The constant value you can use instead of a dsl or ref for this property argument</li>
<li><b>javaCast</b> : If using a java object, you can cast the value of this property argument</li>
<li><b>scope</b> : The scope inside the CFC this property will be injected too. The default scope is the <b>variables</b> scope.</li></ul></td></tr>
<tr>
<td><b>setter</b>([name],[ref],[dsl],[value],[javaCast]) </td>
<td>Used to define all the setter dependencies for a mapped object that follows the JavaBean spec: <i>setXXX</i> where <i>XXX</i> is the name of the mapped object.
<ul>
<li><b>name</b> : The name of the setter. Not used for Java or Webservice construction</li>
<li><b>ref</b> : The mapping reference id this setter is mapped to. E.G. ref='MyFunkyEspresso'</li>
<li><b>dsl</b> : The construction dsl that will be used to construct this setter dependency</li>
<li><b>value</b> : The constant value you can use instead of a dsl or ref for this setter dependency</li>
<li><b>javaCast</b> : If using a java object, you can cast the value of this setter dependency</li></ul></td></tr>
<tr>
<td><b>mixins(udfIncludeList)</b> </td>
<td>A UDF template, a list of templates or an array of templates that WireBox should use to mix-in into the target object. It will take all the methods defined in those UDF templates and mixed them into the target object at runtime.</td></tr>
<tr>
<td><b>providerMethod(method,mapping)</b> </td>
<td>Will inject a new method or override a method on the target object with a new method that provides objects of the mapping you specify.</td></tr>
<tr>
<td><b>virtualInheritance(Mapping)</b> </td>
<td>Create a runtime virtual inheritance from a target object into a target mapping. This approach blends the CFCs together at runtime via mixins and WireBox Funkyness!</td></tr>
<tr>
<td><b>extraAttributes(struct)</b> </td>
<td>Allows the ability to store extra metadata about a mapping into WireBox that can later be retrieved via AOP invocations or WireBox events.</td></tr></tbody></table>

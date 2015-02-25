# Mapping Destinations

The mapping destinations tell WireBox what type of object you are mapping to. You will usually use these methods by concatenating map() or with() initiator calls:

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Method Signature</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>to</b>(path) </td>
<td>Maps a name to a CFC instantiation path</td></tr>
<tr>
<td><b>toDSL</b>(dsl) </td>
<td>Maps a name to DSL builder string. Construction is done by using this DSL string (Look at Injection DSL)</td></tr>
<tr>
<td><b>toFactoryMethod</b>(factory,method) </td>
<td>Maps a name to another mapping (factory) and its method call. If you would like to pass in parameters to this factory method call you will use the <i>methodArg()</i> DSL method concatenated to this method call.</td></tr>
<tr>
<td><b>toJava</b>(path) </td>
<td>Maps a name to a Java class that can be instantiated via <i>createObject("java")</i></td></tr>
<tr>
<td><b>toProvider</b>(provider) </td>
<td>Maps a name to another mapping (provider) that must implement the WireBox Provider interface (<i>coldbox.system.ioc.IProvider</i>)</td></tr>
<tr>
<td><b>toRSS</b>(path) </td>
<td>Maps a name to an atom or RSS URL. WireBox will then use the <i>cffeed</i> tag to construct this RSS feed. It builds out into a structure with two keys:
<ul>
<li><b>metadata</b> : The metadata of the feed</li>
<li><b>items</b> : The items in the feed</li></ul></td></tr>
<tr>
<td><b>toValue</b>(value) </td>
<td>Maps a name to a constant value, which can be ANYTHING.</td></tr>
<tr>
<td><b>toWebservice</b>(path) </td>
<td>Maps a name to a webservice WSDL URL. WireBox will create the webservice via <i>createObject("webservice")</i> for you.</td></tr></tbody></table>

Here are some examples:
```javascript
// CFC
map("FunkyObject").to("myapp.model.service.FunkyService");
mapPath("myapp.model.service.FunkyService");
mapDirectory("myapp.model");
// Java
map("buffer").toJava("java.lang.StringBuffer");
// RSS feed
map("googleNews").toRSS("http://news.google.com/news?output=rss");
// Webservice
map("myWS").toWebservice("http://myapp.com/app.cfc?wsdl");
// Provider
map("Espresso").toProvider("FunkyEspressoProvider");
// DSL
map("Logger").toDSL("logbox:root");

// factory methods
map("ColdboxFactory").to("coldbox.system.extras.ColdboxFactory");
map("ColdBoxController").toFactoryMethod(factory="ColdBoxFactory",method="getColdBox");
map("BeanInjector")
	.toFactoryMethod(factory="ColdBoxFactory",method="getPlugin")
	.methodArg(name="plugin",value="BeanFactory")

// Mixin a new method in my object that dispenses users
mapPath("UserService")
	.providerMethod("getUser","User");
```
<br>
<div style="border: 1px solid black">
<img src="../images/icon_important.png" width="18%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Important : Please note that WireBox can create different types of objects for DI. However, only CFCs will be inspected for autowiring automatically unless you specifically tell WireBox that a certain mapping should not be autowired. In this case you will use the dependencies DSL to define all DI relationships.  </b></p>
<div style="clear:both"></div>
</div>
<br>

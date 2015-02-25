# ColdBox Namespace

This namespace is a combination of namespaces that are only active when used within a ColdBox application:

<table class="tablelisting" cellpadding="”5”,">
<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>coldbox</b> </td>
<td>Get the coldbox controller reference</td></tr>
<tr>
<td><b>coldbox:flash</b> </td>
<td>Get a reference to the application's flash scope object</td></tr>
<tr>
<td><b>coldbox:setting:{setting}</b> </td>
<td>Get the coldbox application <i>{setting}</i> setting and inject it </td></tr>
<tr>
<td><b>coldbox:setting:{setting}@{module}</b> </td>
<td>Get the coldbox application <i>{setting}</i> from the <i>{module}</i> and inject it </td></tr>
<tr>
<td><b>coldbox:plugin:{plugin}</b> </td>
<td>Get the <i>{plugin}</i> plugin and inject it </td></tr>
<tr>
<td><b>coldbox:myPlugin:{MyPlugin}</b> </td>
<td>Get the <i>{MyPlugin}</i> custom plugin and inject it </td></tr>
<tr>
<td><b>coldbox:myPlugin:{MyPlugin}@{module}</b> </td>
<td>Get the <i>{MyPlugin}</i> custom plugin from the {module} module and inject it </td></tr>
<tr>
<td><b>coldbox:datasource:{alias}</b> </td>
<td>Get a new datasource bean according to <i>{alias}</i></td></tr>
<tr>
<td><b>coldbox:configBean</b> </td>
<td>Get a new config bean object and inject it </td></tr>
<tr>
<td><b>coldbox:mailsettingsbean</b> </td>
<td>Get a new mail settings bean and inject it </td></tr>
<tr>
<td><b>coldbox:loaderService</b> </td>
<td>Get a reference to the loader service </td></tr>
<tr>
<td><b>coldbox:requestService</b> </td>
<td>Get a reference to the request service </td></tr>
<tr>
<td><b>coldbox:debuggerService</b> </td>
<td>Get a reference to the debugger service </td></tr>
<tr>
<td><b>coldbox:pluginService</b> </td>
<td>Get a reference to the plugin service </td></tr>
<tr>
<td><b>coldbox:handlerService</b> </td>
<td>Get a reference to the handler service </td></tr>
<tr>
<td><b>coldbox:interceptorService</b> </td>
<td>Get a reference to the interceptor service </td></tr>
<tr>
<td><b>coldbox:moduleService</b> </td>
<td>Get a reference to the ColdBox Module Service</td></tr>
<tr>
<td><b>coldbox:interceptor:{name}</b> </td>
<td>Get a reference of a named interceptor <i>{name}</i></td></tr>
<tr>
<td><b>coldbox:cacheManager</b> </td>
<td>get the cache manager </td></tr>
<tr>
<td><b>coldbox:fwConfigBean</b> </td>
<td>Get a configuration bean object with ColdBox settings instead of Application settings</td></tr>
<tr>
<td><b>coldbox:fwSetting:{setting}</b> </td>
<td>Get a setting from the ColdBox settings instead of the Application settings</td></tr>
<tr>
<td><b>coldbox:moduleSettings:{module}</b> </td>
<td>Inject the entire <i>{module}</i> settings structure</td></tr>
<tr>
<td><b>coldbox:moduleConfig:{module}</b> </td>
<td>Inject the entire <i>{module}</i> configurations structure</td></tr>
<tr>
<td><b>ioc</b> </td>
<td>Get the named ioc bean and inject it. Name comes from the cfproperty, setter or argument name</td></tr>
<tr>
<td><b>ioc:{beanName}</b> </td>
<td>Get the ioc bean according to <i>{beanName}</i></td></tr>
<tr>
<td><b>javaLoader:{class}</b> </td>
<td>Create an object from the <a href="wiki/Plugins:JavaLoader.cfm">JavaLoader</a> plugin and its set of loaded java libraries</td></tr>
<tr>
<td><b>webservice:{alias}</b> </td>
<td>Get a webservice object using an {alias} that matches in your coldbox configuration file.</td></tr></tbody></table>

```javascript
// some examples
property name="logbox" inject="logbox";
property name="rootLogger" inject="logbox:root";
property name="logger" inject="logbox:logger:model.com.UserService";
property name="moduleService" inject="coldbox:moduleService";
property name="producer" inject="coldbox:interceptor:MessageProducer";
property name="configBean" inject="coldbox:fwConfigBean";
property name="producer" inject="interceptor:MessageProducer";
property name="appPath" inject="coldbox:fwSetting:ApplicationPath";

// JavaLoader goodness
property name="binaryHeap" inject="javaLoader:org.apache.commons.collections.BinaryHeap";
property name="email" inject="javaLoader:org.apache.commons.mail.SimpleEmail";
```

# WireBox Namespace

Talk and get objects from the current wirebox injector

<table class="tablelisting" cellpadding="”5”,">
<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>wirebox</b> </td>
<td>Get a reference to the current injector</td></tr>
<tr>
<td><b>wirebox:parent</b> </td>
<td>Get a reference to the parent injector (if any)</td></tr>
<tr>
<td><b>wirebox:eventManager</b> </td>
<td>Get a reference to injector's event manager</td></tr>
<tr>
<td><b>wirebox:binder</b> </td>
<td>Get a reference to the injector's binder</td></tr>
<tr>
<td><b>wirebox:populator</b> </td>
<td>Get a reference to a WireBox's Object Populator utility</td></tr>
<tr>
<td><b>wirebox:scope:{scope}</b> </td>
<td>Get a direct reference to an internal or custom scope object</td></tr>
<tr>
<td><b>wirebox:properties</b> </td>
<td>Get the entire properties structure the injector is initialized with. If running within a ColdBox context then it is the structure of application settings</td></tr>
<tr>
<td><b>wirebox:property:{name}</b> </td>
<td>Retrieve one key of the properties structure</td></tr></tbody></table>

```javascript
property name="beanFactory" inject="wirebox";
property name="settings" inject="wirebox:properties";
property name="singletonCache" inject="wirebox:scope:singleton";
property name="populator" inject="wirebox:populator";
property name="binder" inject="wirebox:binder";
```

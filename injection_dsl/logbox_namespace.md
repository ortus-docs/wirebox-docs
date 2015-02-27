# LogBox Namespace
This DSL namespace interacts with the loaded LogBox instance.

<table class="tablelisting" cellpadding="”5”,">
Interact with LogBox<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>logbox</b> </td>
<td>Get a reference to the application's LogBox instance</td></tr>
<tr>
<td><b>logbox:root</b>	</td>
<td>Get a reference to the root logger</td></tr>
<tr>
<td><b>logbox:logger:{category name}</b> </td>
<td>Get a reference to a named logger by its category name</td></tr>
<tr>
<td><b>logbox:logger:{this}</b> </td>
<td>Get a reference to a named logger using the current target object's path as the category name</td></tr></tbody></table>

```javascript
property name="logbox" inject="logbox";
property name="log" inject="logbox:root";
property name="log" inject="logbox:logger:myapi";
property name="log" inject="logbox:logger:{this}";
```

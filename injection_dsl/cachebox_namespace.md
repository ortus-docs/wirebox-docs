# CacheBox Namespace
This DSL namespace is only active if using CacheBox or a ColdBox application context.

<table class="tablelisting" cellpadding="”5”,">
<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>cachebox</b> </td>
<td>Get a reference to the application's CacheBox instance</td></tr>
<tr>
<td><b>cachebox:{name}</b> </td>
<td>Get a reference to a named cache inside of CacheBox</td></tr>
<tr>
<td><b>cachebox:{name}:{objectKey}</b> </td>
<td>Get an object from the named cache inside of CacheBox according to the objectKey</td></tr></tbody></table>

```javascript
property name="cacheFactory" inject="cacheBox";
property name="cache" inject="cachebox:default";
property name="data" inject="cachebox:default:myKey";
```

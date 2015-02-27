# Provider Namespace
Inject object providers, please refer to our [provider section](../providers/README.md) in this guide.

<table class="tablelisting" cellpadding="”5”,">
<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>provider</b> </td>
<td>Build an object provider that will return the mapping according to the property, method or argument name.</td></tr>
<tr>
<td><b>provider:{name}</b> </td>
<td>Build an object provider that will return the <i>{name}</i> mapping.</td></tr>
<tr>
<td><b>provider:{injectionDSL}</b> </td>
<td>Build an object provider that will return the object that the <i>{injectionDSL}</i> refers to</td></tr></tbody></table>

```javascript
// using id
property name="timedService" inject="provider:TimedService";

// using DSL
property name="timedService" inject="provider:logbox:logger:{this}";
```

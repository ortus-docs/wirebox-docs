# ID-Model-Empty Namespace

The default namespace is not specifying one. This namespace is used to retreive either named mappings or full component paths.

<table class="tablelisting" cellpadding="”5”,">
<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>empty</b> </td>
<td>Same as saying <i>id</i>. Get a mapped instance with the same name as defined in the property, argument or setter method.</td></tr>
<tr>
<td><b>id</b> </td>
<td>Get a mapped instance with the same name as defined in the property, argument or setter method.</td></tr>
<tr>
<td><b>id:{name}</b> </td>
<td>Get a mapped instance by using the second part of the DSL as the mapping name.</td></tr>
<tr>
<td><b>id:{name}:{method}</b> </td>
<td>Get the {name} instance object, call the {method} and inject the results </td></tr>
<tr>
<td><b>model</b> </td>
<td>Get a mapped instance with the same name as defined in the property, argument or setter method. </td></tr>
<tr>
<td><b>model:{name}</b> </td>
<td>Get a mapped instance by using the second part of the DSL as the mapping name.</td></tr>
<tr>
<td><b>model:{name}:{method}</b> </td>
<td>Get the {name} instance object, call the {method} and inject the results </td></tr></tbody></table>


```javascript
// Let's assume we have mapped a few objects called: UserService, SecurityService and RoleService

// Empty inject, use the property name, argument name or setter name
property name="userService" inject;

// Using the name of the mapping as the value of the inject
property name="security" inject="SecurityService";

// Using the full namespace
property name="userService" inject="id:UserService";
property name="userService" inject="model:UserService";

// Simple factory method
property name="roles" inject="id:RoleService:getRoles";
```

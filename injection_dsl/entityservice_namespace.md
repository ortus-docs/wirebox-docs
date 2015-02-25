# EntityService Namespace
Gives you the ability to easily inject base orm services or binded virtual entity services for you:

<table class="tablelisting" cellpadding="”5”,">
<tbody><tr>
<th><b>DSL</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>entityService</b> </td>
<td>Inject a <b>BaseORMService</b> object for usage as a generic service layer</td></tr>
<tr>
<td><b>entityService:{entity}</b> </td>
<td>Inject a <b>VirtualEntityService</b> object for usage as a service layer based off the name of the entity passed in.</td></tr></tbody></table>

```javascript
// Generic ORM service layer
property name="genericService" inject="entityService";
// Virtual service layer based on the User entity
property name="userService" inject="entityService:User";
```

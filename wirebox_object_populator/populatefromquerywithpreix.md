# populateFromQueryWithPrefix


Populates an Object using only specific columns from a query. Useful for performing a query with joins that needs to populate multiple objects.

<h4 style="color:blue">Returns</h4>

* This function returns any

<h4 style="color:blue">Arguments</h4>

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Key</b> </th>
<th><b>Type</b> </th>
<th><b>Required</b> </th>
<th><b>Default</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td>target </td>
<td>any </td>
<td>Yes </td>
<td>--- </td>
<td>This can be an instantiated bean object or a bean instantiation path as a string. If you pass an instantiation path and the bean has an 'init' method. It will be executed. This method follows the bean contract (set{property_name}). Example: setUsername(), setfname()</td></tr>
<tr>
<td>qry </td>
<td>query </td>
<td>Yes </td>
<td>--- </td>
<td>The query to populate the bean object with</td></tr>
<tr>
<td>rowNumber </td>
<td>Numeric </td>
<td>No </td>
<td>1 </td>
<td>The query row number to use for population</td></tr>
<tr>
<td>scope </td>
<td>string </td>
<td>No </td>
<td>
</td><td>Use scope injection instead of setters population. Ex: scope=variables.instance.</td></tr>
<tr>
<td>trustedSetter </td>
<td>boolean </td>
<td>No </td>
<td>false </td>
<td>If set to true, the setter method will be called even if it does not exist in the bean</td></tr>
<tr>
<td>include </td>
<td>string </td>
<td>No </td>
<td>
</td><td>A list of keys to include in the population</td></tr>
<tr>
<td>exclude </td>
<td>string </td>
<td>No </td>
<td>
</td><td>A list of keys to exclude in the population</td></tr>
<tr>
<td>prefix </td>
<td>string </td>
<td>Yes </td>
<td>--- </td>
<td>The prefix used to filter, Example: 'user_' would apply to the following columns: 'user_id' and 'user_name' but not 'address_id'.</td></tr>
<tr>
<td>ignoreEmpty </td>
<td>boolean </td>
<td>No </td>
<td>false </td>
<td>Ignore empty values on populations, great for ORM population</td></tr>
<tr>
<td>nullEmptyInclude </td>
<td>string </td>
<td>No </td>
<td>
</td><td>A list of keys to NULL when empty</td></tr>
<tr>
<td>nullEmptyExclude </td>
<td>string </td>
<td>No </td>
<td>
</td><td>A list of keys to NOT NULL when empty</td></tr>
<tr>
<td>composeRelationships </td>
<td>boolean </td>
<td>No </td>
<td>false </td>
<td>Automatically attempt to compose relationships from memento</td></tr></tbody></table>

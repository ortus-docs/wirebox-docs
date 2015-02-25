# populateFromXML

Populate an object from an XML packet

<h4 style="color:blue">Retunres</h4>
* This function returns <i>any</i>

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
<td>The target to populate</td></tr>
<tr>
<td>xml </td>
<td>any </td>
<td>Yes </td>
<td>--- </td>
<td>The XML string or packet</td></tr>
<tr>
<td>root </td>
<td>string </td>
<td>No </td>
<td>
</td><td>The XML root element to start from</td></tr>
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




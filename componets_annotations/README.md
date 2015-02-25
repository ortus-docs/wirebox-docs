# Componets Annotations

The following are all the annotations that are discovered by WireBox on any component declaration that WireBox constructs:

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Annotation</b> </th>
<th><b>Type</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>autowire</b> </td>
<td>boolean </td>
<td>All objects are marked as autowire=true, so if you want to disable autowiring, you can add this annotation as <b>false</b>. You do NOT need to add this annotation if you want to autowire it, it is redundant if you do.</td></tr>
<tr>
<td><b>alias</b> </td>
<td>string </td>
<td>A list of aliased names you can attach to a CFC instance apart from its Component name. This is great when using the <i>mapDirectory()</i> binder function.</td></tr>
<tr>
<td><b>eagerInit</b> </td>
<td>none </td>
<td>All objects are lazy loaded unless they are marked with this annotation or marked as eager init in the binder configuration.</td></tr>
<tr>
<td><b>threadSafe</b> </td>
<td>none or boolean </td>
<td>Determines the locking construction of the object for its wiring of dependencies. Please see our <i>Object Persistence &amp; Thread Safety</i> Section.</td></tr>
<tr>
<td><b>scope</b> </td>
<td>string </td>
<td>A valid WireBox scope or a custom registered scope. Remember that ALL components by default are placed in the <b>NO SCOPE</b> scope. This means they are considered transient objects.</td></tr>
<tr>
<td><b>singleton</b> </td>
<td>none </td>
<td>Marks a component as a singleton object.</td></tr>
<tr>
<td><b>cachebox</b> </td>
<td>string </td>
<td>Marks a component to be stored in CacheBox. The value of this annotation should be a valid registered CacheBox cache provider. The default cache provider is called <i>default</i></td></tr>
<tr>
<td><b>cache</b> </td>
<td>boolean </td>
<td>Marks a component to be cached in CacheBox in the <i>default</i> provider.</td></tr>
<tr>
<td><b>cacheTimeout</b> </td>
<td>numeric </td>
<td>The timeout in minutes when the object is stored in the CacheBox provider</td></tr>
<tr>
<td><b>cacheLastAccessTimeout</b> </td>
<td>numeric </td>
<td>The timeout in minutes when the object is stored in the CacheBox provider</td></tr>
<tr>
<td><b>mixins</b> </td>
<td>list </td>
<td>A list of UDF templates to mixin into the object</td></tr></tbody></table>



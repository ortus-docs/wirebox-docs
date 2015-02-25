# Mapping Initiators
Ok, now that we know how to configure WireBox, let's get into the fun stuff of object mapping. How do we do this? By using our DSL mapping initiators that tell WireBox how to start the object registration process. You will then concatenate the initiators with some DSL destinations methods, DI data, etc to tell WireBox all the information it might need to construct, wire and persist the object. Here are the DSL initiators:

<table class="tablelisting" cellpadding="5">
<tbody><tr>
<th><b>Method Signature</b> </th>
<th><b>Description</b> </th></tr>
<tr>
<td><b>map</b>(alias) </td>
<td>The method that starts the mapping process. You pass in a mapping name or a list of names to start registering.</td></tr>
<tr>
<td><b>mapPath</b>(path) </td>
<td>Map a CFC instantiation path. This method internally delivers a two-fold punch of doing <i>map('CFCFileName').to(path)</i>. This is a quick way to map a CFC instantiation path that uses the name of the CFC as the mapping name.</td></tr>
<tr>
<td><b>mapDirectory</b>(packagePath,[include],[exclude], [influence], [filter]) </td>
<td>A cool method that tells WireBox to automatically register ALL the CFCs found recursively in that instantiation package path. All CFCs will be registered using their CFC names as the mapping names and WireBox will inspect all the CFCs immediately for DI metadata. The <b>include</b> and <b>exclude</b> arguments can be used for inclusions/exclusions lists via regex. The <i>influence</i> argument can be a UDF or closure that will affect the iterating registrations of objects. The <i>filter</i> argument can be a UDF or closure that will filter out or in the CFCs found, an include/exclude on steroids.</td></tr>
<tr>
<td><b>unMap</b>(alias) </td>
<td>Unmap/delete a mapping in the binder.</td></tr>
<tr>
<td><b>with</b>(alias) </td>
<td>This method is a utility method that retrieves the <i>alias</i> mapping so you can start concatenating methods for that specific mapping. Basically putting it into a workable context.</td></tr></tbody></table>

<br>
<div style="border: 1px solid black">
<img src="../images/icon_important.png" width="10%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
Important: From the methods we have seen above only the map() and with() methods require a DSL destination. </b></p>
<div style="clear:both"></div>
</div>
<br>



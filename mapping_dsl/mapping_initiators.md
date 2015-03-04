# Mapping Initiators

Ok, now that we know how to configure WireBox, let's get into the fun stuff of object mapping. How do we do this? By using our DSL mapping initiators that tell WireBox how to start the object registration process. You will then concatenate the initiators with some DSL destinations methods, DI data, etc to tell WireBox all the information it might need to construct, wire and persist the object. Here are the DSL initiators:


|Method Signature|Description|
|--|--|
|<b>map</b>(alias)|The method that starts the mapping process. You pass in a mapping name or a list of names to start registering|
|<b>mapPath</b>(path)|Map a CFC instantiation path. This method internally delivers a two-fold punch of doing <i>map('CFCFileName').to(path)</i>. This is a quick way to map a CFC instantiation path that uses the name of the CFC as the mapping name|
|<b>mapDirectory</b>(packagePath,[include],[exclude], [influence], [filter])|A cool method that tells WireBox to automatically register ALL the CFCs found recursively in that instantiation package path. All CFCs will be registered using their CFC names as the mapping names and WireBox will inspect all the CFCs immediately for DI metadata. The <b>include</b> and <b>exclude</b> arguments can be used for inclusions/exclusions lists via regex. The <i>influence</i> argument can be a UDF or closure that will affect the iterating registrations of objects. The <i>filter</i> argument can be a UDF or closure that will filter out or in the CFCs found, an include/exclude on steroids|
|<b>unMap</b>(alias)|Unmap/delete a mapping in the binder|
|<b>with</b>(alias)|This method is a utility method that retrieves the <i>alias</i> mapping so you can start concatenating methods for that specific mapping. Basically putting it into a workable context|

<br>
> **Important** From the methods we have seen above only the `map()` and `with()` methods require a DSL destination.



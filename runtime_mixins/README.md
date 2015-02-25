# Runtime Mixins()

<img src="../images/runtime_Mixins.jpg">

You can use the mixins() binder method or mixins annotation to define that a mapping should be mixed in with one or more set of templates. It will then at runtime inject all the methods in those templates and mix them into the target object as public methods.

```javascript
// map with mixins
map("MyService")
	.to("model.UserService")
	.mixins("/helpers/base");

// map with mixins as list
map("MyService")
	.to("model.UserService")
	.mixins("/helpers/base, /helpers/model");

// map with mixins as array
map("MyService")
	.to("model.UserService")
	.mixins( ["/helpers/base", "/helpers/model"] );


// Via annotation
component mixins="/helpers/base"{

}
```

This will grab all the methods in the base.cfm and model.cfm templates and inject them into the target mapping as public methods. Awesome right?

<div style="border: 1px solid black">
<img src="../images/icon_info.png" width="5%" style="float:left;margin-top:10px"><p style="margin:12px"><b>
The list of templates can include a .cfm or not</b></p>
<div style="clear:both"></div>
</div>

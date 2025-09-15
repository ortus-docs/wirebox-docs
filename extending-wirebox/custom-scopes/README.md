# Custom Scopes

WireBox allows you to create your own object persistence scopes so you can have full control on their lifecycle. This is easily done in the following process:

1. Create a CFC that implements `wirebox.system.ioc.scopes.IScope`
2. Register your custom scope in your configuration binder

You can create your own persistence scope or if you are getting funky, override the internal persistence scopes with your own logic.

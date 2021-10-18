# Virtual Inheritance

![](../.gitbook/assets/virtual\_Inheritance.jpg)

You can make two CFCs blend together simulating a virtual runtime inheritance with WireBox. WireBox will grab the target CFC and blend into it all of the virtual inheritance CFC's methods and properties. It will then also create a `$super` reference in the target and a `$superinit()` reference. This is a great alternative to real inheritance and allow for runtime mixins to occur. You start off by mapping the base or source CFC and then mapping the target CFC and declaring a virtualInheritance to the base or source CFC:

```javascript
// Declare base CFC
map("BaseModel").to("model.base.BaseModel");

map("UserService").to("model.users.UserService").virtualInheritance("BaseModel");
```

This will grab all methods and properties in the `BaseModel` CFC and mix them into the `UserService`, then create a virtual `$super` scope which will map to an instantiated instance of the `BaseModel` object.

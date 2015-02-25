# Instance Creations

<img src="../images/instance_mappings.jpg" style="margin-left:75px">

We have now coded our classes and unit tests with some cool annotations in record time, so what do we do next? Well, WireBox works on the idea of three ways to discover and create your classes:

| Approach |	Motivation | Pros | Cons |
| -- | -- | -- | -- | 	
| Implicit Mappings | To replace `createObject()` or `new` calls | Very natural as you just request an object by its instantiation path. Very fast prototyping.  | Refactoring is very hard as code is plagued with instantiation paths everywhere. Not DRY. |
| Explicit Mappings | To replace `createObject()` calls with named keys  | DRY, you can create multiple named mappings that point to the same blueprint of a class. Create multiple iterations of the same class. Very nice decoupling. | Not as fast to prototype as we need to define our mappings before hand in our configuration binder. |
| Scan Locations | CFC discovery by conventions | A partial instantiation path(s) or folder(s) are mapped so you can retrieve by shorthand names. Very quick to prototype also without using full instantiation paths. Override of implementations can be easily done by discovery.  | Harder concept to digest, not as straightforward as implicit and explicit locations. |


So let's do examples for each where our classes we just built are placed in a directory called model of the root directory.

**Implicit Creation**
```javascript
injector = createObject("component","wirebox.system.ioc.Injector").init();
espresso = injector.getInstance("model.CoffeeShop").makeEspresso();

```
<br>
**Explicit Binder Configuration**
```javascript
map("CoolShop").to("model.CoffeeShop");
```
<br>
**Explicit Creation**
```javascript
injector = createObject("component","wirebox.system.ioc.Injector").init();
espresso = injector.getInstance("CoolShop").makeEspresso();
```
<br>
**Scan Locations Binder Configuration**
```javascript
wirebox.scanLocations = ["model"];
```
<br>
**Set Locations Creation**
```javascript
injector = createObject("component","wirebox.system.ioc.Injector").init();
espresso = injector.getInstance("CoffeeShop").makeEspresso();;
```

<br>
So our recommendation is to always try to create configuration binders as best practice, but your requirements might dictate something else.

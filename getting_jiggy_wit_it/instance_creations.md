# Instance Creations

<img src="../images/instance_mappings.jpg" style="margin-left:75px">

We have now coded our classes and unit tests with some cool annotations in record time, so what do we do next? Well, WireBox works on the idea of three ways to discover and create your classes:

<table>
    <tr>
        <th>Apprach</th>
        <th>Motivation</th>
        <th>Pros</th>
        <th>Cons</th>
    </tr>
    <tr>
        <td>Implicit Mappings</td>
        <td>To replace createObject() calls</td>
        <td>Very natural as you just request an object by its instantiation path. Very fast prototyping. </td>
        <td>Refactoring is very hard as code is plagued with instantiation paths everywhere. Not DRY.</td>
    </tr>
        <td>Explicit Mappings</td>
        <td>To replace createObject() calls with named keys </td>
        <td>DRY, you can create multiple named mappings that point to the same blueprint of a class. Create multiple iterations of the same class. Very nice decoupling.</td>
        <td>Not as fast to prototype as we need to define our mappings before hand in our configuration binder.</td>
    </tr>
    </tr>
        <td>Scan Locations</td>
        <td>CFC discovery by conventions</td>
        <td>A partial instantiation path(s) or folder(s) are mapped so you can retrieve by shorthand names. Very quick to prototype also without using full instantiation paths. Override of implementations can be easily done by discovery. </td>
        <td>Harder concept to digest, not as straightforward as implicit and explicit locations.</td>
    </tr>
</table>

So let's do examples for each where our classes we just built are placed in a directory called model of the root directory.

<p style="color:grey">Implicit Creation</p>
```javascript
injector = createObject("component","wirebox.system.ioc.Injector").init();
espresso = injector.getInstance("model.CoffeeShop").makeEspresso();

```
<br>
<p style="color:grey">Explicit Binder Configuration</p>
```javascript
map("CoolShop").to("model.CoffeeShop");
```
<br>
<p style="color:grey">Explicit Creation</p>
```javascript
injector = createObject("component","wirebox.system.ioc.Injector").init();
espresso = injector.getInstance("CoolShop").makeEspresso();
```
<br>
<p style="color:grey">Scan Locations Binder Configuration</p>
```javascript
wirebox.scanLocations = ["model"];
```
<br>
<p style="color:grey">Set Locations Creation</p>
```javascript
injector = createObject("component","wirebox.system.ioc.Injector").init();
espresso = injector.getInstance("CoffeeShop").makeEspresso();;
```
<br>
So our recommendation is to always try to create configuration binders as best practice, but your requirements might dictate something else.

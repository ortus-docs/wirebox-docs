# Common Methods

The following chart shows you the most common methods when dealing with the WireBox Injector. This doesn't mean there are no other methods on the Injector that are of value, so please check out the CFC Docs for more in-depth knowledge.

<table>
    <tr>
        <th>Method Singature</th>
        <th>Comments</th>
    </tr>
    <tr>
        <td>autowire(target,[mapping],[targetID],[annotationCheck]) </td>
        <td>A method you can use to send objects to get autowired by convention or mapping lookups</td>
    </tr>
    <tr>
        <td>clearSingletons() </td>
        <td>A utility method that clears all the singletons from the singleton persistence scope. Great to do in development.</td>
    </tr>
    <tr>
        <td>containsInstance(name) </td>
        <td>Checks if an instance can be created by this Injector or not</td>
    </tr>
    <tr>
        <td>getBinder() </td>
        <td>Get the configuration binder for this injector</td>
    </tr>
    <tr>
        <td>getInstance([name],[dsl],[initArguments]) </td>
        <td>The main method that asks the injector for an object instance by name or by autowire DSL string.</td>
    </tr>
    <tr>
        <td>getObjectPopulator() </td>
        <td>Retrieve the ColdBox object populator that can populate objects from JSON, XML, structures and much more.</td>
    </tr>
    <tr>
        <td>getParent() </td>
        <td>Get a reference to the parent injector (if any)</td>
    </tr>
    <tr>
        <td>getScope(name) </td>
        <td>Get a reference to a registered persistence scope</td>
    </tr>
    <tr>
        <td>setParent(injector) </td>
        <td>Set a parent injector into the target injector to create hierarchies</td>
    </tr>
</table>

# Injector Constructor Arguments

The injector can be constructed with three optional arguments:

<table>
    <tr>
        <th>Argument</th>
        <th>Type</th>
        <th>Required</th>
        <th>Default</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>binder</td>
        <td>instance or instatiation path</td>
        <td>false</td>
        <td>wirebox.system.ioc.config.DefaultBinder </td>
        <td>The binder instance or instantiation path to be used to configure this WireBox injector with</td>
    </tr>
    <tr>
        <td>properties</td>
        <td>struct</td>
        <td>false</td>
        <td>structnew()</td>
        <td>A structure of name value pairs usually used for configuration data that will be passed to the binder for usage in configuration.</td>
    </tr>
    <tr>
        <td>coldbox</td>
        <td>coldbox.system.web.Controller</td>
        <td>false</td>
        <td>null</td>
        <td>A reference to the ColdBox application context you will be linking the Injector to.</td>
    </tr>
</table>

If you are using WireBox within a ColdBox application, you don't even need to do any of this, we do it for you by using some configuration data in your ColdBox configuration file or conventions.

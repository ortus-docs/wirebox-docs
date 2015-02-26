# Injector Constructor Arguments

The injector can be constructed with three optional arguments:

| Argument | Type | Required | Default | Description
| -- | -- | -- | -- | -- |
| binder | instance or instatiation path | false | `wirebox.system.ioc.config.DefaultBinder`  | The binder instance or instantiation path to be used to configure this WireBox injector with |
| properties | struct | false | structnew() | A structure of name value pairs usually used for configuration data that will be passed to the binder for usage in configuration. |
| coldbox | `coldbox.system.web.Controller` | false | null | A reference to the ColdBox application context you will be linking the Injector to.

If you are using WireBox within a ColdBox application, you don't even need to do any of this, we do it for you by using some configuration data in your ColdBox configuration file or conventions.

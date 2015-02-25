# Custom DSL Builder

WireBox allows you to create your own DSL object builders and then register them via your configuration binder. This allows you to create a namespace or override an internal namespace with your own object builder. By now we have seen our injection DSL and noticed that we have internal namespaces. With this feature we can alter it or create new ones so our annotations and injection DSLs can be customized to satisfaction. This is easily done in the following process

1. Create a CFC that implements coldbox.system.ioc.dsl.IDSLBuilder
2. Register your custom DSL builder in your configuration binder

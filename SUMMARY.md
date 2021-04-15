# Table of contents

* [Introduction](README.md)

## Intro

* [Release History](intro/introduction/README.md)
  * [What's New With 6.3.0](intro/introduction/whats-new-with-6.3.0.md)
  * [What's New With 6.2.0](intro/introduction/whats-new-with-5.5.0.md)
  * [What's New With 6.1.0](intro/introduction/whats-new-with-5.4.0.md)
  * [What's New With 6.0.0](intro/introduction/whats-new-with-5.3.0.md)

---

* [About This Book](about-this-book.md)
* [Author](author.md)

## Getting Started

* [Overview](getting-started/overview.md)
* [Installing WireBox](getting-started/installing-wirebox.md)
* [Getting Jiggy Wit It!](getting-started/getting-jiggy-wit-it/README.md)
  * [Instance Creations](getting-started/getting-jiggy-wit-it/instance-creations.md)
  * [Binder Introduction](getting-started/getting-jiggy-wit-it/binder-introduction.md)
  * [Scoping](getting-started/getting-jiggy-wit-it/scoping.md)
  * [Eager Init](getting-started/getting-jiggy-wit-it/eager-init.md)
  * [How WireBox Resolves Dependencies](getting-started/getting-jiggy-wit-it/how-wirebox-resolves-dependencies.md)

## Configuration

* [Configuring WireBox](configuration/configuring-wirebox/README.md)
  * [Binder Configuration Properties](configuration/configuring-wirebox/binder-configuration-properties.md)
  * [Binder Environment Properties](configuration/configuring-wirebox/binder-environment-properties.md)
  * [ColdBox Enhanced Binder](configuration/configuring-wirebox/coldbox-enhanced-binder.md)
  * [Types & Scopes](configuration/configuring-wirebox/types-and-scopes.md)
  * [Data Configuration Settings](configuration/configuring-wirebox/data-configuration-settings.md)
  * [Programmatic Configuration](configuration/configuring-wirebox/programmatic-configuration.md)
* [Mapping DSL](configuration/mapping-dsl/README.md)
  * [Mapping Initiators](configuration/mapping-dsl/mapping-initiators.md)
  * [Mapping Destinations](configuration/mapping-dsl/mapping-destinations.md)
  * [MapDirectory\(\) Influence & Filters](configuration/mapping-dsl/mapdirectory-influence-and-filters.md)
  * [Persistence DSL](configuration/mapping-dsl/persistence-dsl.md)
  * [Dependencies DSL](configuration/mapping-dsl/dependencies-dsl/README.md)
    * [Mapping Extra Attributes](configuration/mapping-dsl/dependencies-dsl/mapping-extra-attributes.md)
  * [Mapping DSL Examples](configuration/mapping-dsl/mapping-dsl-examples.md)
  * [Influence Instances at Runtime](configuration/mapping-dsl/influence-instances-at-runtime.md)
  * [Processing Mappings](configuration/mapping-dsl/processing-mappings.md)
* [Component Annotations](configuration/component-annotations/README.md)
  * [Persistence Annotations](configuration/component-annotations/persistence-annotations.md)
  * [CacheBox Annotations](configuration/component-annotations/cachebox-annotations.md)
* [Parent Object Definitions](configuration/parent-object-definitions.md)

## Usage

* [WireBox Injector](usage/wirebox-injector/README.md)
  * [Injector Constructor Arguments](usage/wirebox-injector/injector-constructor-arguments.md)
  * [Injection Idioms](usage/wirebox-injector/injection-idioms.md)
  * [Common Methods](usage/wirebox-injector/common-methods.md)
* [Injection DSL](usage/injection-dsl/README.md)
  * [ColdBox Namespace](usage/injection-dsl/coldbox-namespace.md)
  * [CacheBox Namespace](usage/injection-dsl/cachebox-namespace.md)
  * [EntityService Namespace](usage/injection-dsl/entityservice-namespace.md)
  * [Executor Namespace](usage/injection-dsl/executor-namespace.md)
  * [Java Namespace](usage/injection-dsl/java-namespace.md)
  * [LogBox Namespace](usage/injection-dsl/logbox-namespace.md)
  * [Models Namespace](usage/injection-dsl/id-model-empty-namespace.md)
  * [Provider Namespace](usage/injection-dsl/provider-namespace.md)
  * [WireBox Namespace](usage/injection-dsl/wirebox-namespace.md)
* [WireBox Event Model](usage/wirebox-event-model/README.md)
  * [WireBox Events](usage/wirebox-event-model/wirebox-events.md)
  * [WireBox Listeners](usage/wirebox-event-model/wirebox-listeners/README.md)
    * [ColdBox Mode Listener](usage/wirebox-event-model/wirebox-listeners/coldbox-mode-listener.md)
    * [Standalone Mode Listener](usage/wirebox-event-model/wirebox-listeners/standalone-mode-listener.md)

## Advanced Topics

* [Providers](advanced-topics/providers/README.md)
  * [Custom Providers](advanced-topics/providers/custom-providers.md)
  * [toProvider\(\) closures](advanced-topics/providers/toprovider-closures.md)
  * [Virtual Provider Injection DSL](advanced-topics/providers/virtual-provider-injection-dsl.md)
  * [Virtual Provider Mapping](advanced-topics/providers/virtual-provider-mapping.md)
  * [Virtual Provider Lookup Methods](advanced-topics/providers/virtual-provider-lookup-methods.md)
  * [Provider onMissingMethod Proxy](advanced-topics/providers/provider-onmissingmethod-proxy.md)
  * [Scope Widening Injection](advanced-topics/providers/scope-widening-injection.md)
* [Virtual Inheritance](advanced-topics/virtual-inheritance.md)
* [Runtime Mixins\(\)](advanced-topics/runtime-mixins.md)
* [Object Persistence & Thread Safety](advanced-topics/object-persistence-and-thread-safety.md)
* [ORM Entity Injection](advanced-topics/orm-entity-injection.md)
* [WireBox Object Populator](advanced-topics/wirebox-object-populator/README.md)
  * [populateFromXML](advanced-topics/wirebox-object-populator/populatefromxml.md)
  * [populateFromQuery](advanced-topics/wirebox-object-populator/populatefromquery.md)
  * [populateFromStruct](advanced-topics/wirebox-object-populator/populatefromstruct.md)
  * [populateFromQueryWithPrefix](advanced-topics/wirebox-object-populator/populatefromquerywithprefix.md)
  * [populateFromJSON](advanced-topics/wirebox-object-populator/populatefromjson.md)

## Extending WireBox

* [Custom DSL](extending-wirebox/custom-dsl/README.md)
  * [The DSL Builder Interface](extending-wirebox/custom-dsl/the-dsl-builder-interface.md)
  * [Registering a Custom DSL](extending-wirebox/custom-dsl/registering-a-custom-dsl.md)
* [Custom Scopes](extending-wirebox/custom-scopes/README.md)
  * [The Scope Interface](extending-wirebox/custom-scopes/the-scope-interface.md)
  * [Scoping Process](extending-wirebox/custom-scopes/scoping-process.md)
  * [Registering a Custom Scope](extending-wirebox/custom-scopes/registering-a-custom-scope.md)
* [WireBox Injector Interface](extending-wirebox/wirebox-injector-interface.md)

## Aspect Oriented Programming

* [AOP Intro](aspect-oriented-programming/aop-intro/README.md)
  * [Overview](aspect-oriented-programming/aop-intro/overview/README.md)
    * [AOP Vocabulary](aspect-oriented-programming/aop-intro/overview/aop-vocabulary.md)
  * [Activate The AOP Listener](aspect-oriented-programming/aop-intro/activate-the-aop-listener.md)
  * [Create Your Aspect](aspect-oriented-programming/aop-intro/create-your-aspect/README.md)
    * [MethodInvocation Useful Methods](aspect-oriented-programming/aop-intro/create-your-aspect/methodinvocation-useful-methods.md)
    * [MethodLogger Aspect](aspect-oriented-programming/aop-intro/create-your-aspect/methodlogger-aspect.md)
  * [Aspect Registration](aspect-oriented-programming/aop-intro/aspect-registration.md)
  * [Aspect Binding](aspect-oriented-programming/aop-intro/aspect-binding.md)
  * [Auto Aspect Binding](aspect-oriented-programming/aop-intro/auto-aspect-binding/README.md)
    * [ClassMatcher Annotation DSL](aspect-oriented-programming/aop-intro/auto-aspect-binding/classmatcher-annotation-dsl.md)
    * [MethodMatcher Annotation DSL](aspect-oriented-programming/aop-intro/auto-aspect-binding/methodmatcher-annotation-dsl.md)
  * [Included Aspects](aspect-oriented-programming/aop-intro/included-aspects/README.md)
    * [CFTransaction](aspect-oriented-programming/aop-intro/included-aspects/cftransaction.md)
    * [HibernateTransaction](aspect-oriented-programming/aop-intro/included-aspects/hibernatetransaction.md)
    * [MethodLogger](aspect-oriented-programming/aop-intro/included-aspects/methodlogger.md)
  * [Summary](aspect-oriented-programming/aop-intro/summary.md)


# Summary

## Intro

* [Introduction](README.md)
  * [What's New With 5.0.0](whats-new-with-500.md)
  * [What's New With 2.1.0](whats-new-with-2.1.0.md)
  * [What's New With 2.0.0](whats-new-with-2.0.0.md)
  * [About This Book](about-this-book.md)
  * [Author](author.md)

## Getting Started

* [Overview](overview/README.md)
* [Installing WireBox](installing-wirebox.md)
* [Getting Jiggy Wit It!](getting-jiggy-wit-it/README.md)
  * [Instance Creations](getting-jiggy-wit-it/instance-creations.md)
  * [Binder Introduction](getting-jiggy-wit-it/binder-introduction.md)
  * [Scoping](getting-jiggy-wit-it/scoping.md)
  * [Eager Init](getting-jiggy-wit-it/eager-init.md)
  * [How WireBox Resolves Dependencies](getting-jiggy-wit-it/how-wirebox-resolves-dependencies.md)

## Configuration

* [Configuring WireBox](configuring-wirebox/README.md)
  * [Binder Configuration Properties](configuring-wirebox/binder-configuration-properties.md)
  * [Binder Environment Properties](configuring-wirebox/binder-environment-properties.md)
  * [ColdBox Enhanced Binder](configuring-wirebox/coldbox-enhanced-binder.md)
  * [Types & Scopes](configuring-wirebox/types-and-scopes.md)
  * [Data Configuration Settings](configuring-wirebox/implicit-configuration-settings.md)
  * [Programmatic Configuration](mapping-dsl/wirebox-configuration.md)
* [Mapping DSL](mapping-dsl/README.md)
  * [Mapping Initiators](mapping-dsl/mapping-initiators/README.md)
    * [MapDirectory\(\) Influence & Filters](mapping-dsl/mapping-initiators/mapdirectory-influence-and-filters.md)
  * [Mapping Destinations](mapping-dsl/mapping-destinations.md)
  * [Persistence DSL](mapping-dsl/persistence-dsl.md)
  * [Dependencies DSL](mapping-dsl/dependencies-dsl/README.md)
    * [Mapping Extra Attributes](mapping-dsl/dependencies-dsl/mapping-extra-attributes.md)
  * [Mapping DSL Examples](mapping-dsl/mapping-dsl-examples.md)
  * [Influence Instances at Runtime](mapping-dsl/influence-instances-at-runtime.md)
* [Component Annotations](component-annotations/README.md)
  * [Persistence Annotations](component-annotations/persistence-annotations.md)
  * [CacheBox Annotations](component-annotations/cachebox-annotations.md)
* [Parent Object Definitions](parent-object-definitions.md)

## Usage

* [WireBox Injector](wirebox-injector/README.md)
  * [Injector Constructor Arguments](wirebox-injector/injector-constructor-arguments.md)
  * [Injection Idioms](wirebox-injector/injection-idioms.md)
  * [Common Methods](wirebox-injector/common-methods.md)
* [Injection DSL](injection-dsl/README.md)
  * [ID-Model-Empty Namespace](injection-dsl/id-model-empty-namespace.md)
  * [Provider Namespace](injection-dsl/provider-namespace.md)
  * [WireBox Namespace](injection-dsl/wirebox-namespace.md)
  * [CacheBox Namespace](injection-dsl/cachebox-namespace.md)
  * [EntityService Namespace](injection-dsl/entityservice-namespace.md)
  * [LogBox Namespace](injection-dsl/logbox-namespace.md)
  * [Java Namespace](injection-dsl/java-namespace.md)
  * [ColdBox Namespace](injection-dsl/coldbox-namespace.md)
* [WireBox Event Model](wirebox-event-model/README.md)
  * [WireBox Events](wirebox-event-model/wirebox-events.md)
  * [WireBox Listeners](wirebox-event-model/wirebox-listeners/README.md)
    * [ColdBox Mode Listener](wirebox-event-model/wirebox-listeners/coldbox-mode-listener.md)
    * [Standalone Mode Listener](wirebox-event-model/wirebox-listeners/standalone-mode-listener.md)

## Advanced Topics

* [Providers](providers/README.md)
  * [Custom Providers](providers/custom-providers.md)
  * [toProvider\(\) closures](providers/toprovider-closures.md)
  * [Virtual Provider Injection DSL](providers/virtual-provider-injection-dsl.md)
  * [Virtual Provider Mapping](providers/virtual-provider-mapping.md)
  * [Virtual Provider Lookup Methods](providers/virtual-provider-lookup-methods.md)
  * [Provider onMissingMethod Proxy](providers/provider-onmissingmethod-proxy.md)
  * [Scope Widening Injection](providers/scope-widening-injection.md)
* [Virtual Inheritance](virtual-inheritance.md)
* [Runtime Mixins\(\)](runtime-mixins.md)
* [Object Persistence & Thread Safety](object-persistence-and-thread-safety.md)
* [ORM Entity Injection](orm-entity-injection.md)
* [WireBox Object Populator](wirebox-object-populator/README.md)
  * [populateFromXML](wirebox-object-populator/populatefromxml.md)
  * [populateFromQuery](wirebox-object-populator/populatefromquery.md)
  * [populateFromStruct](wirebox-object-populator/populatefromstruct.md)
  * [populateFromQueryWithPreix](wirebox-object-populator/populatefromquerywithpreix.md)
  * [populateFromJSON](wirebox-object-populator/populatefromjson.md)

## Extending WireBox

* [Custom DSL](custom-dsl/README.md)
  * [The DSL Builder Interface](custom-dsl/the-dsl-builder-interface.md)
  * [Registering a Custom DSL](custom-dsl/registering-a-custom-dsl.md)
* [Custom Scopes](custom-scopes/README.md)
  * [The Scope Interface](custom-scopes/the-scope-interface.md)
  * [Scoping Process](custom-scopes/scoping-process.md)
  * [Registering a Custom Scope](custom-scopes/registering-a-custom-scope.md)
* [WireBox Injector Interface](wirebox-injector-interface.md)

## Aspect Oriented Programming

* [Aspect Oriented Programming](aspect-oriented-programming/README.md)
  * [Overview](aspect-oriented-programming/overview/README.md)
    * [AOP Vocabulary](aspect-oriented-programming/overview/aop-vocabulary.md)
  * [Activate The AOP Listener](aspect-oriented-programming/activate-the-aop-listener.md)
  * [Create Your Aspect](aspect-oriented-programming/create-your-aspect/README.md)
    * [MethodInvocation Useful Methods](aspect-oriented-programming/create-your-aspect/methodinvocation-useful-methods.md)
    * [MethodLogger Aspect](aspect-oriented-programming/create-your-aspect/methodlogger-aspect.md)
  * [Aspect Registration](aspect-oriented-programming/aspect-registration.md)
  * [Aspect Binding](aspect-oriented-programming/aspect-binding.md)
  * [Auto Aspect Binding](aspect-oriented-programming/auto-aspect-binding/README.md)
    * [ClassMatcher Annotation DSL](aspect-oriented-programming/auto-aspect-binding/classmatcher-annotation-dsl.md)
    * [MethodMatcher Annotation DSL](aspect-oriented-programming/auto-aspect-binding/methodmatcher-annotation-dsl.md)
  * [Included Aspects](aspect-oriented-programming/included-aspects/README.md)
    * [CFTransaction](aspect-oriented-programming/included-aspects/cftransaction.md)
    * [HibernateTransaction](aspect-oriented-programming/included-aspects/hibernatetransaction.md)
    * [MethodLogger](aspect-oriented-programming/included-aspects/methodlogger.md)
  * [Summary](aspect-oriented-programming/summary.md)


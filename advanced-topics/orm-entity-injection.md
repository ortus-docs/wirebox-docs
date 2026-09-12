# ORM Entity Injection

BoxLang is the preferred language for new ColdBox/WireBox applications, and its ORM approach differs from the legacy CFML/Hibernate pattern below. Pick the tab that matches your engine.

{% hint style="info" %}
WireBox uses a per-request transient injection cache by default, so repeated `autowire()` calls for the same entity mapping during a request reuse the resolved injections and delegations. You can disable this globally via `transientInjectionCache` or per-entity with the `transientCache="false"` annotation.
{% endhint %}

{% tabs %}
{% tab title="BoxLang" %}
### BoxLang ORM (bx-orm)

BoxLang's ORM module lets you declare a persistent entity directly as a class, using standalone `@persistent`/`@entityName` annotations instead of a `.cfc`-style `cfclocation` setting:

```js
@entityName( "Auto" )
@persistent
class {
    property name="id"    type="string" fieldtype="id" ormtype="string";
    property name="make"  type="string";
    property name="model" type="string";
}
```

There is currently no documented automatic `@inject`-on-property support for ORM-managed entities (entities are instantiated by Hibernate, not by WireBox), so the safe, documented pattern is to look up WireBox-managed services manually from inside an entity lifecycle hook (`onPreInsert()`, `onPreUpdate()`, `onPreDelete()`) via the application-scoped injector:

```js
@entityName( "Auto" )
@persistent
class {
    property name="id"    type="string" fieldtype="id" ormtype="string";
    property name="make"  type="string";
    property name="model" type="string";

    function onPreInsert(){
        var pricingService = application.wirebox.getInstance( "services.PricingService" );
        pricingService.applyDefaults( this );
    }
}
```

{% hint style="warning" %}
This page's manual-lookup pattern reflects what's currently documented for `bx-orm`. If a future `bx-orm` release adds first-class WireBox property injection on entities (mirroring `@inject` on regular classes), this page will be updated to match.
{% endhint %}
{% endtab %}
{% tab title="CFML" %}
### Custom ORM Event Handler

On CFML/Hibernate, entity injection is done via a custom ORM event handler rather than on the entity itself. Activate event handling in `Application.cfc`:

```cfscript
this.ormSettings = {
    cfclocation="model",
    dbcreate = "update",
    dialect = "MySQLwithInnoDB",
    logSQL = true,
    // Enable event handling
    eventhandling = true,
    // Set the event handler to use, which will be inside our application or the default wirebox one
    eventhandler = "model.ORMEventHandler"
};
```

Then create the custom event handler with a `postLoad()` function that leverages WireBox for DI:

```cfscript
component implements="CFIDE.orm.IEventHandler"{

    /**
    * postLoad called by hibernate which in turn announces a coldbox interception: ORMPostLoad
    */
    public void function postLoad(any entity){
        application.wirebox.autowire(
            target=arguments.entity,
            targetID="ORMEntity-#getMetadata( arguments.entity ).name#"
        );
    }

}
```
{% endtab %}
{% endtabs %}

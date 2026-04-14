# Injection DSL

The injection DSL is a domain specific language that denotes what to inject in the current placeholder: property, argument, or method via the inject annotation. This injection DSL not only can it be used via annotations but also via our mapping DSL whenever a `dsl` argument can be used. This DSL is constructed by joining words separated by a `:` colon. The first part of this string is what we will denote as the injection **DSL Namespace**.

```
inject="{namespace}:extra:extra:extra"
```

## Property Annotation

Every property can be annotated with our injection annotations:

* `inject` : The injection DSL
* `scope` : The visibility scope to inject the dependency into. By default it injects into `variables` scope

{% tabs %}
{% tab title="BoxLang" %}
```java
property name="service" inject="id:MyService";

property name="TYPES" inject="id:CustomTypes" scope="this";

property name="roles" inject="id:RoleService:getRoles" scope="instance";
```
{% endtab %}
{% tab title="CFML" %}
```javascript
property name="service" inject="id:MyService";

property name="TYPES" inject="id:CustomTypes" scope="this";

property name="roles" inject="id:RoleService:getRoles" scope="instance";
```
{% endtab %}
{% endtabs %}

## Constructor Argument Annotation

You can also annotate constructor arguments with the inject annotation:

{% tabs %}
{% tab title="BoxLang" %}
```java
/**
 * @myService.inject UserService
 * @cache.inject    cachebox:default
 */
function init( required myService, required cache ){
}
```
{% endtab %}
{% tab title="CFML" %}
```javascript
/**
 * @myService.inject UserService
 * @cache.inject     cachebox:default
 */
function init( required myService, required cache ){
}
```
{% endtab %}
{% endtabs %}

## Setter Method Annotation

You can also annotate setter methods with the inject annotation to provide injections:

{% tabs %}
{% tab title="BoxLang" %}
```java
function setService( required service ) inject="UserService" {
    variables.service = arguments.service
}
```
{% endtab %}
{% tab title="CFML" %}
```javascript
function setService( required service ) inject="UserService" {
    variables.service = arguments.service;
}
```
{% endtab %}
{% endtabs %}

WireBox offers a wide gamut of annotation namespaces you can use in your BoxLang and CFML applications and ColdBox applications. However, we took it a step further and allowed you to create your own custom DSL namespaces making your annotations come alive!

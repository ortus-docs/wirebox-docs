# Injection DSL

The injection DSL is a domain specific language that denotes what to inject in the current placeholder: property, argument, or method via the inject annotation. This injection DSL not only can it be used via annotations but also via our mapping dsl whenever a dsl argument can be used. This DSL is constructed by joining words separated by a : colon. The first part of this string is what we will denote as the injection DSL Namespace.

```javascript
inject="{namespace}:extra:extra:extra"
```


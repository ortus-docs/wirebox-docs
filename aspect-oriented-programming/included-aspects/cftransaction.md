# CFTransaction

This aspect is a self-binding aspect that will surround methods with simple ColdFusion transaction blocks.

| ClassMatcher | MethodMatcher |
| --- | --- |
| any | annotatedWith:transactional |

To use, just declare in your binder, overriding the self-binding is totally optional.

```javascript
mapAspect("CFTransaction").to("coldbox.system.aop.aspects.CFTransaction");
```


# What's New With 6.2.0

This minor release brings in some major performance enhancements for the way WireBox maps and creates objects.  We highly encourage upgrading to it.

## Compatibility Notes

If you are using annotations for component **aliases** you will have to tell WireBox explicitly to process those mappings.  As by default, we no longer process mappings on startup.

```javascript
map( name ).process();
```

## New Feature

* \[[WIREBOX-84](https://ortussolutions.atlassian.net/browse/WIREBOX-84)\] - Remove auto processing of all mappings defer to lazy loading
* \[[WIREBOX-85](https://ortussolutions.atlassian.net/browse/WIREBOX-85)\] - `MapDirectory` new boolean argument `process` which defers to **false**, if **true**, the mappings will be auto processed
* \[[WIREBOX-86](https://ortussolutions.atlassian.net/browse/WIREBOX-86)\] - New binder method: `process()` if chained from a mapping, it will process the mapping's metadata automatically.

## Improvement

* \[[WIREBOX-87](https://ortussolutions.atlassian.net/browse/WIREBOX-87)\] - AOP debug logging as serialized CFCs which clogs log files


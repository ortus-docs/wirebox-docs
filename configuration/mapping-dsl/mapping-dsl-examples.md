# Mapping DSL Examples

```javascript
mapPath("path")
mapDSL("cool", "model.CoolFactory");

map("SecurityService")
    .to("model.security.SecurityService")
    .onDICOmplete(["start","executeRoles"])

mapDirectory('/shared/model');

 // Eager initialized objects
map("luis,joe").to("model.Luis").into(this.SCOPES.SINGLETON).asEagerInit()
map(["luis","joe"]).to("model.Luis").into(this.SCOPES.SINGLETON).asEagerInit()

// map a property to a mapping id via DSL
map("Lui").toDSL("coldbox:setting:luis")

// using initWith() for passing name-value pairs or positional arguments for direct initialization of a mapping
map("transferConfig")
    .to("transfer.com.config.Configuration")
    .initWith(datasourcePath=getProperty('datasourcePath'),
           configPath=getProperty('configPath'),
          definitionPath=getProperty('definitionPath'));

// Now doing with setter injection
map("transferConfig")
    .to("transfer.com.config.Configuration")
    .setter(name="datasourcePath", value=getProperty("datasourcePath"))
    .setter(name="configPath", value=getProperty("datasourcePath"))
    .setter(name="definitionPath", value=getProperty("definitionPath") );


// Map with constructor arguments
map("transfer")
    .to("transfer.com.Transfer")
    .into(SCOPES.SINGLETON)
    .noAutowire()
    .asEagerInit()
    .initArg(name="configuration",ref='transferConfig');  //ref = name by default, or have an explicit name

// RSS Integration With Caching.
map("googleNews")
    .toRSS("http://news.google.com/news?pz=1&ned=us&hl=en&topic=h&num=3&output=rss")
    .asEagerInit()
    .inCacheBox(timeout=20,lastAccessTimeout=30,provider="default",key="google-news");

// Java Integration with init arguments
map("Buffer").
    toJava("java.lang.StringBuffer").
    initArg(value="500",javaCast="long");

// Java integration with initWith() custom arguments and your own casting.
map("Buffer").
    toJava("java.lang.StringBuffer").
    initWith( javaCast("long",500) );
```


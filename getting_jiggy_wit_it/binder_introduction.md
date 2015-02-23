# Binder Introduction

<img src="../images/binderIntro_WireboxBinder.jpg" style="margin-left:90px">

In all reality we could be building our objects and its dependencies, [object graph](http://en.wikipedia.org/wiki/Object_graph), without any configuration just plain location and implicit conventions. This is great but not very flexible for refactoring, so let's do the best practice of defining a mapping or an alias to a real object. We do this by creating a WireBox configuration binder (wirebox.system.ioc.config.Binder), which is a simple CFC that defines the way WireBox behaves and defines object mappings. This binder is then used to initialize WireBox so it has knowledge of these mappings and our settings.


###### Wirebox Binder and Configuration Introduction video
<a href="http://f.vimeocdn.com/p/flash/moogaloop/6.0.37/moogaloop.swf?clip_id=20938425&z=1424728141463"><img src="../images/binderIntro_VideoThumbnail.png" width="80%"></a>

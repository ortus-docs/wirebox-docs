# WireBox Event Model

WireBox also sports a very nice event model that can announce several object life cycle events. You can listen to these events and interact with WireBox at runtime very easily, whether you are in standalone mode or within a ColdBox application.

> **Note** If you are within a ColdBox application, you get the benefit of all the potential of [ColdBox Interceptors](https://coldbox.ortusbooks.com/full/interceptors/interceptors.html) and if you are in standalone mode, well, you just get the listener and that's it.

Each event execution also comes with a structure of name-value pairs called `interceptData` that can contain objects, variables and all kinds of data that can be useful for listeners to use. This data is sent by the event caller and each event caller decides what this data sent is. Also, remember that WireBox also can be ran with a reference to [CacheBox](https://cachebox.ortusbooks.com), which also offers lots of internal events that you can tap into. So let's start investigating first the object life cycle events.

![](../../.gitbook/assets/event_Model%20%281%29.jpg)


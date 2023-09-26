# WireBox Event Model

WireBox also sports event-driven programming where it can announce several object life cycle events, and you can listen to them by creating listener CFCs.

{% hint style="success" %}
**Note:** If you are within a ColdBox application, you get the benefit of all the potential of [ColdBox Interceptors](https://coldbox.ortusbooks.com/full/interceptors/interceptors.html), and if you are in standalone mode, well, you get the listener, and that's it.
{% endhint %}

Each event execution also comes with a structure of name-value pairs called `data` that can contain objects, variables, and all kinds of data useful for listeners. This data is sent by the event caller, and each event caller decides what this data sent is. Also, remember that WireBox can also be run with a reference to [CacheBox](https://cachebox.ortusbooks.com), which also offers lots of internal events you can tap into. So, let's start investigating first the object's life cycle events.

![](../../.gitbook/assets/event\_Model.jpg)

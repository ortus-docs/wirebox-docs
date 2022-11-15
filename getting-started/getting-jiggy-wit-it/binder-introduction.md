# Binder Introduction

![](<../../.gitbook/assets/binderIntro\_WireBoxBinder (1) (1).jpg>)

In all reality we could be building our objects and its dependencies, [object graph](http://en.wikipedia.org/wiki/Object\_graph), without any configuration just plain **location** and **implicit** conventions. This is great but not very flexible for refactoring, so let's do the best practice of defining a mapping or an alias to a real object.

We do this by creating a WireBox configuration binder `wirebox.system.ioc.config.Binder`, which is a simple CFC that defines the way WireBox behaves and defines object mappings. This binder is then used to initialize WireBox so it has knowledge of these mappings and our settings.

{% hint style="info" %}
The Binder is also the way you configure WireBox for operation.
{% endhint %}

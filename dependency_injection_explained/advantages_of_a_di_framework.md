# Advantages of a DI Framework

Compared to manual DI, using WireBox can lead to the following advantages:

* You will write less boilerplate code.
* By giving WireBox DI responsibilities, you will stop creating objects manually or using custom object factories.
* You can leverage object persistence scopes for performance and scalability. Even create time persisted objects.
* You will not have any object creation or wiring code in your application, but have it abstracted via WireBox. Which will lead to more cohesive code that is not plagued with boilerplate code or factory code.
* Objects will become more testable and easier to mock, which in turn can accelerate your development by using a TDD (Test Driven Development) approach.
* Once WireBox leverages your objects you can take advantage of AOP or other event life cycle processes to really get funky with OO.

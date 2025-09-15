# WireBox Events

WireBox's offers a wide gamut of life cycle events that are announced at certain points in execution time. Below are the current events announced by the Injector `wirebox.system.ioc.Injector`.

| **Event**                  | **Data**                                                 | **Description**                                                                                                                                                                           |
| -------------------------- | -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| afterInjectorConfiguration | **injector** : The calling injector reference            | Called right after the injector has been fully configured for operation.                                                                                                                  |
| beforeInstanceCreation     | **mapping** : The mapping called to be created           | Called right before an object mapping is built via our internal object builders or custom scope builders.                                                                                 |
| afterInstanceInitialized   | **mapping** : The mapping called to be created           | Called after an object mapping gets constructed and initialized. The mapping has NOT been placed on a scope yet and no DI/AOP has been performed yet                                      |
| afterInstanceCreation      | **mapping** : The mapping called to be created           | Called once the object has been fully created, initialized, stored, and DI/AOP performed on it. It is about to be returned to the caller via its getInstance() method.                    |
| beforeInstanceInspection   | **mapping** : The mapping that is about to be processed. | Called whenever an object has been requested and its metadata has not been processed or discovered. In this interception point you can influence the metadata discovery.                  |
| afterInstanceInspection    | **mapping** : The mapping that is about to be processed. | Called after an object mapping has been completely processed with its DI metadata discovery. This is your last chance to change or modify the DI data in the mapping before it is cached. |
| beforeInjectorShutdown     | **injector** : The calling injector reference            | Called right before the Injector instance is shutdown.                                                                                                                                    |
| afterInjectorShutdown      | **injector** : The calling injector reference            | Called right after the Injector instance is shutdown.                                                                                                                                     |
| beforeInstanceAutowire     | **injector** : The calling injector reference            | Called right after the instance has been created and initialized, but before DI wiring is done.                                                                                           |
| afterInstanceAutowire      | **injector** : The calling injector reference            | Called right after the instance has been created, initialized and DI has been completed on it.                                                                                            |

{% hint style="info" %}
Please see our [CacheBox](http://cachebox.ortusbooks.com) documentation to see all of CacheBox's events.
{% endhint %}

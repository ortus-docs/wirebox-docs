# Binder Environment Properties

The WireBox binder will also be injected with 3 methods that will allow you to talk to your system environment or Java system properties.  This will help you with container based applications or applications that rely on environment settings/secrets.

* `getEnv( key, [defaultValue] )` - Get a Java system environment value
* `getSystemProperty( key, [defaultValue] )` - Get a Java system property value
* `getSystemSetting( key, [defaultValue] )` - This method will retrieve a key from the Java system properties and if it does not exist, then it checks the system environment.


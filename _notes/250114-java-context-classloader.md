---
layout: default
title: Context Class Loader
---

# Context Class Loader

These are my notes from [Difference between thread's context class loader and normal classloader](https://stackoverflow.com/q/1771679).

Generally, never use the context class loader. If you have to call a method that is missing a `ClassLoader` parameter, set it to `getClass().getClassLoader()`. 

When code from one class asks to load another class, the correct class loader to use is the same class loader as the caller class, i.e. `getClass().getClassLoader()`. This is the way things work 99.9% of the time because this is what the JVM does itself the first time you construct an instance of a new class, invoke a static method, or access a static field.

When you want to create a class using reflection (such as when deserializing or loading a configurable named class), the library that does the reflection should always ask the application which class loader to use, by receiving the `ClassLoader` as a parameter from the application. The application (which would know all the classes that it wants to construct) should pass it `getClass().getClassLoader()`.

Any other way to obtain a class loader is incorrect. If a library uses hacks such as `Thread.getContextClassLoader()`, `sun.misc.VM.latestUserDefinedLoader()`, or `sun.reflect.Reflection.getCallerClass()` it is a bug caused by a deficiency in the API. `Thread.getContextClassLoader()` exists only because whoever designed the `ObjectInputStream` API forgot to accept the `ClassLoader` as a parameter, and this mistake has continued to haunt the Java community.

That said, several JDK classes use one of a few hacks to decide the class loader to be used. Some use the `ContextClassLoader` (which fails when you run different apps on a shared thread pool, or when you leave the `ContextClassLoader` `null`), some walk the stack (which fails when the direct caller of the class is itself a library), some use the system class loader (which is fine, as long as it is documented to only use classes in the `CLASSPATH`) or bootstrap class loader, and some use an unpredictable combination of the above techniques (which makes things more confusing). For example,
  - JNDI uses context classloaders
  - Class.getResource() and Class.forName() use the current classloader
  - JAXP uses context classloaders (as of J2SE 1.4)
  - java.util.ResourceBundle uses the caller's current classloader
  - URL protocol handlers specified via java.protocol.handler.pkgs system property are looked up in the bootstrap and system classloaders only
  - Java Serialization API uses the caller's current classloader by default

When using such an API, first try to find an overload of the method that accepts the class loader as a parameter. If there is no sensible method, then try setting the `ContextClassLoader` before the API call, and reset it afterwards. For example,
``` java
ClassLoader originalClassLoader = Thread.currentThread().getContextClassLoader();
try {
    Thread.currentThread().setContextClassLoader(getClass().getClassLoader());
    // call some API that uses reflection without taking ClassLoader param
} finally {
    Thread.currentThread().setContextClassLoader(originalClassLoader);
}
```

---
layout: default
title: What's new in Java 7?
---

# What's new in Java 7?
##### 14-Mar-2021

This is my perspective on _What's new in Java 7_ &mdash; about new things that I am interested in. For a full documentation of features and enhancements in Java 7, refer the [release notes](https://www.oracle.com/java/technologies/javase/jdk7-relnotes.html).

## Swing

### Customize Swing components using `JLayer` class
The new `JLayer` class allows you to draw on components and respond to component events without modifying the underlying component directly. For more details, refer the Java Tutorial [How to Decorate Components with the JLayer Class](https://docs.oracle.com/javase/tutorial/uiswing/misc/jlayer.html).

### Nimbus Look & Feel
Nimbus Look & Feel is now a public API. It uses Java 2D vector graphics to draw the user interface, instead of static bitmaps. So the user interface works well with high resolution displays. Nimbus is customizable &mdash; you can change the size of components to 3 levels, change the color theme, or customize the rendering of components with your own _skins_. For more details, refer the Java Tutotrial [Nimbus Look and Feel](https://docs.oracle.com/javase/tutorial/uiswing/lookandfeel/nimbus.html).

### Mixing heavyweight and lightweight components is easier
Now, in most cases, mixing heavyweight and lightweight components just works. To know the requirements for the mixing to work, and the limitations when it would not work, refer this [technical article](https://www.oracle.com/technical-resources/articles/java/mixing-components.html). 

### Translucent and Shaped Windows
You can now create translucent and shaped windows. This is of course subject to support from the underlying platform. For more details, refer the Java Tutorial [How to Create Translucent and Shaped Windows](https://docs.oracle.com/javase/tutorial/uiswing/misc/trans_shaped_windows.html)

## Security

### Support for Elliptic Curve Cryptography
ECC is becoming popular, particularly for resource-constrained environments such as mobile or wireless. Compared to RSA, ECC offers equivalent security with smaller key sizes. This results in savings in consumption of CPU, power, memory, and bandwidth. A new provider in Java 7 provides several ECC-based algorithms (ECDSA/ECDH). This removes the requirement to use external libraries for accessing ECC functionality.

### Server Name Indication (SNI) for JSSE client
Java 7 supports the Server Name Indication (SNI) extension in the JSSE client. This enables java-based TLS clients to connect to virtual servers.

## Internationalization

### Unicode 6.0 support
Java 7 supports Unicode 6.0.0, which adds support for over 2000 additional characters.

### Unicode 6.0 Support in Regular Expressions API
The Regular Expressions API in Java 7 has been enhanced to support Unicode 6.0. You can match Unicode code points using the RegEx API. You must use \u or \x escape sequences.

## Java 2D

### XRender-Based Rendering Pipeline
A new XRender-based Java 2D rendering pipeline is supported for modern X11-based desktops. It offers improved graphics performance. By default, the pipeline is disabled. To enabled, set the property `-Dsun.java2d.xrender=true`. Note that, the older X11 configurations may not be able to support XRender. The property setting `-Dsun.java2d.xrender=True` may be used to enable a message to STDOUT, which will indicate whether the pipeline was actually enabled or not.

### Support for Linux Fonts
For Windows, the logical fonts for the JDK are defined in the fontconfig.properties file. On Linux, there is no guarantee of the presence of specific fonts to support specific locales. Java 7 uses libfontconfig to select the fonts to be used for the logical fonts on Linux platforms. Refer [Fontconfig](https://www.freedesktop.org/wiki/Software/fontconfig/) for more information.


---
layout: default
title: What's new in Java 7
---

# What's new in Java 7
##### 03-Oct-2020

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

### Miscellaneous
JColorChooser component now supports Hue-Saturation-Luminance (HSL) color model.


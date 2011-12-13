.. _best-practice-screen-size:

Dealing with multiple screen sizes
==================================

When creating mobile apps it is important to consider that different devices have different resolutions, aspect ratios, pixel densities and potential orientations. This page describes some techniques which may be used to handle these, however none of these remove the need for testing your app on a varity of devices.

The Android developer documentation has a far more detailed document on how multiple screen types are supported by Android: http://developer.android.com/guide/practices/screens_support.html.

Scalable or not
---------------

An important question to consider when designing your page is whether or not certain parts of the page should be able to dynamically resize (or scale) depending on the screen they are displayed. In some situations the width of an element needs to be fixed, but a paragaph of text may display in a perfectly readable way at several different widths.

If your elements can be resized then it may be as simple as using a relative size when describing them in CSS, such as ``width: 80%``. If you required fixed size elements then you may wish to consider detecting the screen size and render content appropriately. A way this can be done using CSS3 is using media queries, which is described in more detail on http://css-tricks.com/6731-css-media-queries/.

Common screen sizes
-------------------

Some of the most common screen sizes to be considered for mobile development are given below, all sizes are given in the number of points (or CSS pixels) which are available to the webview.

* iPhone
 * Vertical: 320x460
 * Horizontal: 480x300
* iPad
 * Vertical: 768x1004
 * Horizonal: 1024x748

Glossary
--------

Below we define some of the terms used in this page.

pixel
  The smallest physical square that can be displayed on a screen, importantly a pixel in css does not always measure a physical pixel used on the device.

aspect ratio
  The ratio of width to height on a screen, this can vary significantly on mobile devices, and also changes when the device is rotated.
  
pixel density
  Different devices have different sizes of physical pixels, on Android devices are grouped into different desities of pixels, so that different devices can display the same content at a similar physical size. On iOS devices with a retina display have double the pixel density of other devices.
  
display independent pixel or point
  Both of these terms are used to describe the "pixel" size used by CSS and HTML rather than the physical pixel size on Android and iOS devices.
  
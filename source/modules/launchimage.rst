.. _modules-launchimage:

``launchimage``: Launch images
================================================================================

The ``launchimage`` module displays an image while your app is loading.

By default, the launch image is hidden automatically when the window ``load``
event fires - this gives your JavaScript some time to initialise itself, set up
native :ref:`topbars <modules-topbar>` and :ref:`tabbars <modules-tabbar>` for
example.

However, if you want full control over hiding the launch image yourself, set
``hide-manually`` to ``true`` (see below).

Config
------

Images to be displayed during launch as required on iOS, for further details see the `Apple documentation <http://developer.apple.com/library/ios/#documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/App-RelatedResources/App-RelatedResources.html#//apple_ref/doc/uid/TP40007072-CH6-SW12>`_.

On Android the image will be displayed centered on a black background while the first page is loading, as Android device sizes vary a pixel perfect loading image cannot be used. The image will be proportionally scaled down to fit the screen if necessary.

All 4 iOS images must be defined for any to be included in iOS builds. Both Android images must be defined for Android builds.

Properties and image sizes are:

* ``iphone``: 320x480px
* ``iphone-retina``: 640x960px
* ``iphone-retina4``: 640x1136px - for the iPhone 5's four inch screen
* ``ipad``: 768x1004px
* ``ipad-landscape``: 1024x748px
* ``ipad-retina``: 1536x2008px
* ``ipad-landscape-retina``: 2048x1496px
* ``android``
* ``android-landscape``

.. parsed-literal::
    {
        "modules": {
            "launchimage": {
                "iphone": "iphone.png",
                "iphone-retina": "iphone-retina.png",
                "iphone-retina4": "iphone-retina4.png",
                "ipad": "ipad.png",
                "ipad-landscape": "ipad-landscape.png",
                "ipad-retina": "ipad-retina.png",
                "ipad-landscape-retina": "ipad-landscape-retina.png",
                "android": "android.png",
                "android-landscape": "android-landscape.png",
                "hide-manually": true
            }
        }
    }

API
---
``hide``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: launchimage.hide(success, error)

    :param function(content) success: called after the launch image has been hidden
    :param function(content) error: called with details of any error which may occur

If you want to manually hide the launch image yourself, use this API.

You will probably also want to specify ``hide-manually`` in your launchimage
module configuration.

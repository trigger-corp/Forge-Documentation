.. _modules-launchimage:

``launchimage``: Launch images
================================================================================

The ``launchimage`` module displays an image while your app is loading.

Config
------

Images to be displayed during launch as required on iOS, for further details see the `Apple documentation <http://developer.apple.com/library/ios/#documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/App-RelatedResources/App-RelatedResources.html#//apple_ref/doc/uid/TP40007072-CH6-SW12>`_.

On Android the image will be displayed centered on a black background while the first page is loading, as Android device sizes vary a pixel perfect loading image cannot be used. 

All 4 iOS images must be defined for any to be included in iOS builds. Both Android images must be defined for Android builds.

Properties and image sizes are:

* ``iphone``: 320x480px
* ``iphone-retina``: 640x960px
* ``ipad``: 768x1004px
* ``ipad-landscape``: 1024x748px
* ``android``
* ``android-landscape``

.. parsed-literal::
    {
        "modules": {
            "launchimage": {
                "iphone": "iphone.png",
                "iphone-retina": "iphone-retina.png",
                "ipad": "ipad.png",
                "ipad-landscape": "ipad-landscape.png",
                "android": "android.png",
                "android-landscape": "android-landscape.png"
            }
        }
    }
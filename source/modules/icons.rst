.. _modules-icons:

``icons``: App icons
================================================================================

This part of the config allows you to define the icons to be used for your app. All icons are square, and must be placed in your ``src`` directory.

Define your desired icons with ``"size": "path"`` attributes, where ``size`` is the pixel height (and width) of the icon, and ``path`` is where the image has been placed under the ``src`` directory.

.. highlight:: js

You can specify different icons for different platforms as so::

    "android": {
        "36": "icon36.png",
        "48": "icon48-android.png"
        "72": "icon72.png"
    },
    "chrome": {
        "16": "icon16.png",
        "48": "icon48-chrome.png"
        "128": "icon128.png
    }

Here, Android and Chrome will share their 16x16 pixel icon, but use different 48x48 pixel icons.

The icons required for each platform are listed below:

* Android: 36px, 48px and 72px
* Chrome: 16px, 48px and 128px
* Firefox: 32px and 64px
* Internet Explorer: 16px ``.ico`` format
* iOS: 57px, 72px, 114px and 144px for home screen icons, 512px to be shown in iTunes.
* Safari: 32px, 48px and 64px with transparent background. See the Creating an Image section in Apple's `Safari extension guide <http://developer.apple.com/library/safari/#documentation/Tools/Conceptual/SafariExtensionGuide/AddingButtonstotheMainSafariToolbar/AddingButtonstotheMainSafariToolbar.html#//apple_ref/doc/uid/TP40009977-CH3-SW1>`_.

.. note:: If you specify *any* icons for a particular platform, you **must** specify all required icons!

.. note:: iOS includes a special ``prerendered`` option, setting this to true will stop iOS from applying the gloss effect to your icons.

Config
------

.. parsed-literal::
    {
        "modules": {
            "icons": {
                "android": {
                    "36": "icon36.png",
                    "48": "icon48-android.png"
                    "72": "icon72.png"
                },
                "ios": {
                    "57": "icon57.png",
                    "72": "icon72-ios.png",
                    "114": "icon114.png",
                    "144": "icon144.png",
                    "prerendered": true
                }
            }
        }
    }

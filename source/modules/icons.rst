.. _modules-icons:

``icons``: App icons
================================================================================

This part of the config allows you to define the icons to be used for your app. All icons are square, and must be placed in your ``src`` directory.

Define your desired icons with ``"size": "path"`` attributes, where ``size`` is the pixel height (and width) of the icon, and ``path`` is where the image has been placed under the ``src`` directory.

.. highlight:: js

You can specify different icons for different platforms as so::

    "android": {
        "16": "icon16.png",
        "32": "icon32.png",
        "48": "icon48-android.png"
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
* Internet Explorer: TODO
* iOS: 57px, 72px, 114px and 144px for home screen icons, 512px to be shown in iTunes.
* Safari: 32px, 48px and 64px

.. note:: If you specify *any* icons for a particular platform, you **must** specify all required icons!

.. note:: iOS includes a special ``prerendered`` option, setting this to true will stop iOS from applying the gloss effect to your icons.

Config
------

.. parsed-literal::
    {
        "modules": {
            "icons": {
                "android": {
                    "16": "icon16.png",
                    "32": "icon32.png",
                    "48": "icon48-android.png"
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
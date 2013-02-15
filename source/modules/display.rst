.. _modules-display:

``display``: App display options
================================================================================

This controls how your app will be displayed as the device is moved around. The default is to allow for any orientation, with the content being re-drawn as the screen is rotated.

Config
------

.. parsed-literal::
    {
        "modules": {
            "display": {
                "orientations": {
                    ":ref:`default <field-orientations_default>`": "any",
                    ":ref:`iphone <field-orientations_iphone>`": "portrait",
                    ":ref:`ipad <field-orientations_ipad>`": "landscape",
                    ":ref:`android <field-orientations_android>`": "landscape",
                }, 
                ":ref:`fullscreen <field-fullscreen>`": {
                    "android": false,
                    "ios": false,
                    "wp": true
                }
            }
        }
    }

.. _field-orientations_default:

You can limit this behaviour by specifying the desired supported orientations as ``orientations.default``, choosing from ``"any"``, ``"portrait"`` or ``"landscape"``.

.. _field-orientations_iphone:

.. _field-orientations_android:

.. _field-orientations_ipad:

You can further customise this behaviour by specifying orientation support for different devices, e.g. ``orientations.iphone`` and ``orientations.ipad``. For example::

  "orientations": {
    "default": "any",
    "iphone": "portrait",
    "ipad": "landscape"
  },

This configuration means

* by default, display your app in any orientation
* ... but on iPhones, only display your app in portrait mode, either way up
* ... and on iPads, your app will only use the landscape orientation
* ... on Android the default will apply and any orientation allowed by the device will be used

.. _field-fullscreen:

The fullscreen option will hide the system statusbar while your app is running and allow your app to run completely fullscreen on the device. Supported device types are:

* ``android``: Android devices
* ``ios``: Both iPhone and iPad devices
* ``wp``: Windows phone devices

API
---

The ``display`` module also allows you to change the orientation limitations while your app is running with the following API.

``orientation.forceLandscape``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Force the app into a landscape orientation.

.. js:function:: display.orientation.forceLandscape(success, error)

    :param function(value) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``orientation.forcePortrait``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Force the app into a portrait orientation.

.. js:function:: display.orientation.forcePortrait(success, error)

    :param function(value) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``orientation.allowAny``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Allow any app orientation.

.. js:function:: display.orientation.allowAny(success, error)

    :param function(value) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

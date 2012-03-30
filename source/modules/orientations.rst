.. _modules-orientations:

``orientations``: Background scripts
================================================================================

This controls how your app will be displayed as the device is moved around. The default is to allow for any orientation, with the content being re-drawn as the screen is rotated.

Config
------

.. parsed-literal::
    {
        "modules": {
            "orientations": {
                ":ref:`default <field-orientations_default>`": "any",
                ":ref:`iphone <field-orientations_iphone>`": "portrait",
                ":ref:`ipad <field-orientations_ipad>`": "landscape",
                ":ref:`android <field-orientations_android>`": "landscape",
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
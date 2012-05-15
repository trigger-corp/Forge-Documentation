.. _modules-requirements:

``requirements``: App requirements
================================================================================

The ``requirements`` module allows you to set specific device requirements for your apps.

Config
------

Currently supported options are a minimum version for Android and iOS.

 * The Android minimum version is the minimum Android API level you want to support, it must be between 5 and 15. More details can be found on the Android developers site: http://developer.android.com/guide/appendix/api-levels.html.
 * The iOS version is the minimum iOS version you want to support, between 4.0 and 5.1.

.. parsed-literal::
    {
        "requirements": {
            "android": {
                "minimum_version": "6"
            },
            "ios": {
                "minimum_version": "4.3"
            }
        }
    }
.. _native_plugins_native_build_steps:

Changing build configuration
============================

Plugins often need to change properties of the app which cannot be set at
runtime, such as app permissions on Android, or linked system frameworks on
iOS. These changes can be described in the native build steps file for each
platform, and will be applied at build time for the Forge app.

The build steps go in either ``android/build_steps.json`` or ``ios/build_steps.json`` in the plugin's folder. These JSON files take the following format::

    [
        {
            "do": {
                "build_task": {
                    "parameter": "value"
                }
            }
        }, {
            "do": {
                "second_build_task": {
                    "input": "data",
                    "other_input": "data2"
                }
            }
        }
    ]

This consists of an array of tasks to perform before the build is completed.

The types of task that can be performed and the parameters that need to be
passed to each task varies by platform and is described below.

Android
-------

``android_add_permission``
~~~~~~~~~~~~~~~~~~~~~~~~~~

* ``permission``: the permission to add, i.e. ``android.permission.CAMERA``

Example::

    {
        "do": {
            "android_add_permission": {
                "permission": "android.permission.CAMERA"
            }
        }
    }

``android_add_feature``
~~~~~~~~~~~~~~~~~~~~~~~

* ``feature``: the feature to request
* ``required``: Whether or not the feature is required, ``"true"`` or
  ``"false"``

Example::

    {
        "do": {
            "android_add_feature": {
                "feature": "android.hardware.camera",
                "required": "true"
            }
        }
    }

``android_add_activity``
~~~~~~~~~~~~~~~~~~~~~~~~

* ``activity_name``: Name of activity
* ``attributes``: Optional attributes

Example::

    {
        "do": {
            "android_add_activity": {
                "activity_name": "com.example.sdk.MyActivity",
                "attributes": {
                    "android:screenOrientation": "portrait"
                }
            }
        }
    }


``android_add_service``
~~~~~~~~~~~~~~~~~~~~~~~

* ``service_name``: Name of service
* ``attributes``: Optional attributes

Example::

    {
        "do": {
            "android_add_service": {
                "activity": "com.example.sdk.MyService"
            }
        }
    }

``android_add_receiver``
~~~~~~~~~~~~~~~~~~~~~~~~

* ``receiver_name``: Name of receiver
* ``attributes``: Optional attributes
* ``intent_filters``: Optional intent filters

Example::

    {
        "do": {
            "android_add_service": {
                "activity": "com.example.sdk.MyReceiver",
                "intent_filters": {
                    "action": "android.intent.action.BOOT_COMPLETED"
                }
            }
        }
    }

iOS
---

``add_ios_system_framework``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* ``framework``: the framework to add

Example::

    {
        "do": {
            "add_ios_system_framework": {
                "framework": "CoreMedia.framework"
            }
        }
    }

``ios_add_url_handler``
~~~~~~~~~~~~~~~~~~~~~~~

* ``scheme``: URL scheme to handle

Example::

    {
        "do": {
            "ios_add_url_handler": {
                "scheme": "myurlscheme"
            }
        }
    }


``set_in_info_plist``
~~~~~~~~~~~~~~~~~~~~~

* ``key``: Key to add/change: you can use ``a.b`` to change key ``b`` nested inside ``a``
* ``value``: Value to set it to

Example::

    {
        "do": {
            "set_in_info_plist": {
                "key": "MyKey",
                "value": "My Data"
            }
        }
    }

.. _modules-package_names:

``package_names``: Built package names
================================================================================

This controls the package name used internally when building your app, you probably don't need to set this unless you want to replace an existing app with a Forge app.

By default, we create a package name for your app, something like ``io.trigger.forge.appname*``. Although your users aren't going to see this value, it can sometimes be useful to be able to control it manually, for example when updating a previous app that wasn't built on Forge.

Config
------

``package_names`` should be an object mapping a target name onto a package name, e.g.::

    "android": "com.example.my_app_name",
    "ios": "com.example.ios.app"

Currently, only ``android`` and ``ios`` are supported.

.. parsed-literal::
    {
        "modules": {
            "package_names": {
                "android": "com.example.app",
                "ios": "com.example.ios.app"
            }
        }
    }
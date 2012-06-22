.. _modules-package_names:

``package_names``: Built package names
================================================================================

This controls the package name used internally when building your app; if you don't set this manually, we'll generate a package name automatically for you, which looks something like ``io.trigger.forge7faf8ebcb8a111e1910212313d1adcbe``.

Although your users aren't really going to see this value, it can be useful
to be able to control it manually, for example when updating a previous app
that wasn't built on Forge, or if you already have iOS provisioning profiles
which don't match our generated ID.

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

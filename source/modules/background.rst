.. _modules-background:

``background``: Background scripts
================================================================================

**Platforms: Browser**

The ``background`` module allows your app to have a persistent Javascript context running in the background

Config
------

Browsers have the :ref:`concept of content scripts and background <extension-concepts>` files.

This field lists the files that should be included in background context.

.. parsed-literal::
    {
        "modules": {
            "background": {
                "files": ["js/background.js"]
            }
        }
    }

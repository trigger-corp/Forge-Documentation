.. _modules-urlhandler:

``urlhandler``: Custom URL schemes
================================================================================

Config
------

The ``urlhandler`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "urlhandler": {
                "scheme": "your.url.scheme"
            }
        }
    }

API
--------------------------------------------

``urlhandler.urlLoaded``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered when the app is loaded by a custom URL scheme.

.. js:function:: urlhandler.urlLoaded.addListener(callback, error)

    :param function({url: url}) callback: callback invoked with details of the url.
    :param function(content) error: called with details of any error which may occur
.. _modules-geolocation:

``geolocation``: Geolocation
================================================================================

Although geolocation APIs are part of the HTML5 specification, on some platforms, the default permissions dialogs can be cumbersome and annoying to your users.

For that reason, we offer an alternative way to get geolocation data.


Config
------

The ``geolocation`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "geolocation": true
        }
    }

API
---

.. js:function:: geolocation.getCurrentPosition(options, success, error)

    :param object options: request specific levels of service from the location provider
    :param function(position) success: called with an object matching the W3C `Position <http://dev.w3.org/geo/api/spec-source.html#coordinates>`_ specification
    :param function(error) error: called when the user chooses not to share their location with your app

.. note:: To enable easy porting from existing HTML5 code onto Forge, we also accept parameters in the order ``(success, error, options)``



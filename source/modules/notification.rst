.. _modules-notifications:

``notification``: Notifications
===============================

Config
------

The ``notification`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "notification": true
        }
    }

API
---

Notifications allow you to send alerts.

``create``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: notification.create(title, text, success, error)

    :param string title: title
    :param string text: notification message
    :param function() success: success
    :param function(content) error: called with details of any error which may occur

Permissions
-----------

On Chrome this module will add the ``notifications`` permission to your app, users will be prompted to accept this when they install your app.

On Android this module will add the ``VIBRATE`` permission.
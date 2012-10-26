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

``setBadgeNumber``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: iOS**

Allows you to set or remove a badge for your app's icon on the iOS home screen:

.. image:: /_static/images/badge_screenshot.png

If you pass in `0` as number, it will remove this badge. This is particularly useful if you
want to clear a badge set by a push notification.

.. js:function:: notification.setBadgeNumber(number, success, error)

	:param string number: number

Permissions
-----------

On Chrome this module will add the ``notifications`` permission to your app, users will be prompted to accept this when they install your app.

On Android this module will add the ``VIBRATE`` permission.
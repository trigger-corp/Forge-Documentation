.. _notifications:

Notifications: ``forge.notification``
================================================================================

Notifications allow you to send alerts.

``create``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: notification.create(title, text, success, error)

    :param string title: title
    :param string text: notification message
    :param function() success: success
    :param function(content) error: called with details of any error which may occur
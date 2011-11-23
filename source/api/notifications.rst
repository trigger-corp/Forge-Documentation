.. _notifications:

Notifications: ``forge.notification``
================================================================================

Notifications allow you to send alerts.

``create``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Chrome, Firefox, Safari, IE, Android**

.. js:function:: notification.create(title, text, successCallback, errorCallback)

    :param string title: title
    :param string text: notification message
    :param function successCallback: successCallback Receives the X as it's only parameter
    :param function errorCallback: errorCallback Receives an object with message and otherwise undefined schema
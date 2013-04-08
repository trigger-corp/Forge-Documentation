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

``alert``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android, iOS**

Show a dialog window with text content that the user can dismiss. Similar to
using ``window.alert`` except you can control the title text for the dialog.

To create an alert like this:

.. image:: /_static/images/notification_alert_screenshot.png

You would use this code::

  forge.notification.alert("My Title: Alert", "My Body: Alert", function () {
    // ... implement logic for when user dismissed alert
  });

.. js:function:: notification.alert(title, body, success, error)

	:param string title: text to show as the title of the dialog
	:param string body: text to show as the body of the dialog
	:param function() success: called when the user dismisses the alert
	:param function(content) error: called with details of any error which may occur

``confirm``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android, iOS**

Show a dialog window prompting the user with a "yes"/"no" style question.

To show a confirmation dialog like this:

.. image:: /_static/images/notification_confirm_screenshot.png

You would use this code::

  forge.notification.confirm("My Title: Confirm", "My Body: Confirm", "Y", "N", function (userClickedYes) {
    if (userClickedYes) {
      // ... implement logic for when user clicked "Y"
    } else {
      // ... implement logic for when user clicked "N"
    }
  });

.. js:function:: notification.confirm(title, body, positive, negative, success, error)

	:param string title: text to show as the title of the dialog
	:param string body: text to show as the body of the dialog
	:param string positive: text to use for the positive action button
	:param string negative: text to use for the negative action button
	:param function(result) success: called with ``true`` if the user selected the positive option, ``false`` if they selected the negative option.
	:param function(content) error: called with details of any error which may occur

``toast``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android, iOS**

Create a small popup which disappears after a few seconds.

.. image:: /_static/images/notification_toast_screenshot.png

.. js:function:: notification.toast(body, success, error)

	:param string body: body
	:param function() success: called if the toast is displayed successfully
	:param function(content) error: called with details of any error which may occur

Permissions
-----------

On Chrome this module will add the ``notifications`` permission to your app, users will be prompted to accept this when they install your app.

On Android this module will add the ``VIBRATE`` permission.

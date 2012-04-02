.. _partner-parse:

Parse
===============================================================================

"Add a Backend to Your Mobile App in Minutes" - `Parse <https://parse.com/>`_ allows you to add backend features to your mobile app without a server.

Currently Parse push notifications are integrated with Forge.

Config
------

In order for your app to communicate with the Parse servers you must specifiy both your applicationId and clientKey in your apps config.json as shown:

.. parsed-literal::
    {
        "partners": {
            "parse": {
                "applicationId": "YourApplicationKeyZdAtirdSn02Qy6NofiU2Hf",
                "clientKey": "YourClientKeyZdAtirdSn02QQy6NofiU2Hfy6No"
            }
        }
    }

API: ``forge.partners.parse``
-----------------------------

Push notifications received through Parse can be used with the generic push notification event in Forge, see the :ref:`event API <modules-event>` for more details. The following code is an example of how to show an alert to a user when a push notification is recieved.

Example::

    forge.event.messagePushed.addListener(function (msg) {
        alert(msg.alert);
    });

Parse uses channels to send push notifications to specific groups of users, by default all users are subscribed to the empty channel; if you wish to send push notifications to specific users you can use the following methods to manage the channels a user is subscribed to:

push.subscribe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.push.subscribe(channel, success, error)

    :param string channel: Identifier of the channel to subscribe to
    :param function() success: success
    :param function(content) error: called with details of any error which may occur

push.unsubscribe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.push.unsubscribe(channel, success, error)

    :param string channel: Identifier of the channel to unsubscribe from
    :param function() success: success
    :param function(content) error: called with details of any error which may occur

push.subscribedChannels
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.push.subscribedChannels(success, error)

    :param function(channels) success: Called with an array of subscribed channels
    :param function(content) error: called with details of any error which may occur

Permissions
-----------

On Android this module will add the ``VIBRATE`` and ``RECEIVE_BOOT_COMPLETED`` permissions to your app, users will be prompted to accept this when they install your app.

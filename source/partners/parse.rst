.. _partner-parse:

Parse
===============================================================================

"Add a Backend to Your Mobile App in Minutes" - `Parse <https://parse.com/>`_ allows you to add backend features to your mobile app without a server. Their back end features include a datastore, user accounts and push notifications.

Parse push notifications are integrated directly Forge. Other Parse features may be accessed by using :ref:`forge.request.ajax <cross-domain>` with the `Parse REST API <https://parse.com/docs/rest>`_.

Configuring Push Notifications
------------------------------
First you'll need to register an app at `parse.com <https://parse.com/>`_.

In order for your app to communicate with the Parse servers for push notifications you must specifiy both your applicationId and clientKey in your app's :ref:`config.json <api-event>` as shown:

.. parsed-literal::
    "partners": {
        "parse": {
            "applicationId": "YourApplicationKeyZdAtirdSn02Qy6NofiU2Hf",
            "clientKey": "YourClientKeyZdAtirdSn02QQy6NofiU2Hfy6No"
        }
    }

API: ``forge.partners.parse``
-----------------------------

Push notification received through Parse can be used with the generic push notification event in Forge (see the :ref:`event API <api-event>` for more details). The following code is an example of how to show an alert to a user when a push notification is recieved.

Example::

    forge.event.messagePushed.addListener(function (msg) {
        alert(msg.alert);
    });

You can try out sending a push notification from your app's control panel at `parse.com <https://parse.com/>`_.

Parse uses channels to send push notifications to specific groups of users. By default all users are subscribed to the empty channel; if you wish to send push notifications to specific users, you can use the following methods to manage which channels a user is subscribed to.

subscribe
~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.subscribe(channel, success, error)

    :param string channel: Identifier of the channel to subscribe to
    :param function() success: Called if the request is successful
    :param function(content) error: Called with details of any error which may occur

unsubscribe
~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.unsubscribe(channel, success, error)

    :param string channel: Identifier of the channel to unsubscribe from
    :param function() success: Called if the request is successful
    :param function(content) error: Called with details of any error which may occur

subscribedChannels
~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.subscribedChannels(success, error)

    :param function(channels) success: Called with an array of subscribed channels
    :param function(content) error: Called with details of any error which may occur
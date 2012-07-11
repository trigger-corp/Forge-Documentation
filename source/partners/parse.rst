.. _partner-parse:

``push``: notifications (with Parse)
===============================================================================

"Add a Backend to Your Mobile App in Minutes" - `Parse <https://parse.com/>`_ allows you to add backend features to your mobile app without a server. Their back end features include a datastore, user accounts and push notifications.

For a small example on our blog, see `Using Parse and Trigger.io for cross-platform apps without pain in the back-end <http://trigger.io/cross-platform-application-development-blog/2012/03/23/using-parse-and-trigger-io-for-cross-platform-apps-without-pain-in-the-back-end/>`_.

Parse push notifications are integrated directly Forge. Other Parse features may be accessed by using :ref:`forge.request.ajax <modules-request>` with the `Parse REST API <https://parse.com/docs/rest>`_.

Configuring Push Notifications
------------------------------
First you'll need to register an app at `parse.com <https://parse.com/>`_.

In order for your app to communicate with the Parse servers for push notifications you must specifiy both your applicationId and clientKey in your app's :ref:`config.json <modules-event>` as shown:

.. parsed-literal::
    "partners": {
        "parse": {
            "applicationId": "YourApplicationKeyZdAtirdSn02Qy6NofiU2Hf",
            "clientKey": "YourClientKeyZdAtirdSn02QQy6NofiU2Hfy6No"
        }
    }

.. note:: This Parse configuration must go in the *partners* section of your ``config.json``, not *modules* as is the norm with normal Forge modules.

API: ``forge.partners.parse``
-----------------------------

Push notifications received through Parse can be used with the generic push notification event in Forge, see the :ref:`event API <modules-event>` for more details. The following code is an example of how to show an alert to a user when a push notification is received.

Example::

    forge.event.messagePushed.addListener(function (msg) {
        alert(msg.alert);
    });

You can try out sending a push notification from your app's control panel at `parse.com <https://parse.com/>`_.

Parse uses channels to send push notifications to specific groups of users. By default all users are subscribed to the empty channel; if you wish to send push notifications to specific users, you can use the following methods to manage which channels a user is subscribed to.

push.subscribe
~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.push.subscribe(channel, success, error)

    :param string channel: Identifier of the channel to subscribe to
    :param function() success: Called if the request is successful
    :param function(content) error: Called with details of any error which may occur

Example::

    forge.partners.parse.push.subscribe("beta-testers",
    function () {
      forge.logging.info("subscribed to beta-tester push notifications!");
    },
    function (err) {
      forge.logging.error("error subscribing to beta-tester notifications: "+
        JSON.stringify(err));
    });

push.unsubscribe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.push.unsubscribe(channel, success, error)

    :param string channel: Identifier of the channel to unsubscribe from
    :param function() success: Called if the request is successful
    :param function(content) error: Called with details of any error which may occur

Example::

    forge.partners.parse.push.unsubscribe("beta-testers",
    function () {
      forge.logging.info("no more beta-tester notifications...");
    },
    function (err) {
      forge.logging.error("couldn't unsubscribe from beta-tester notifications: "+
        JSON.stringify(err));
    });

push.subscribedChannels
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

.. js:function:: parse.push.subscribedChannels(success, error)

    :param function(channels) success: Called with an array of subscribed channels
    :param function(content) error: Called with details of any error which may occur

Example::

    forge.partners.parse.push.subscribedChannels(
    function (channels) {
      forge.logging.info("subscribed to: "+JSON.stringify(channels));
    },
    function (err) {
      forge.logging.error("couldn't retreive subscribed channels: "+
        JSON.stringify(err));
    });

Permissions
-----------

On Android this module will add the ``VIBRATE`` and ``RECEIVE_BOOT_COMPLETED`` permissions to your app, users will be prompted to accept this when they install your app.

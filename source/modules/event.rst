.. _modules-event:

``event``: Events
================================================================================

Config
------

The ``event`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "event": true
        }
    }

API
--------------------------------------------

The ``forge.event`` namespace allows app to listen for events of interest, which may be triggered multiple times (or potentially not at all) depending on the situation.

``menuPressed.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android**

Triggered when the menu button is pressed on an Android device.

.. js:function:: event.menuPressed.addListener(callback, error)

    :param function() callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``orientationChange.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered when the device is rotated, use forge.is.orientation.portrait() and  forge.is.orientation.landscape() to determine orientation.

.. js:function:: event.orientationChange.addListener(callback, error)

    :param function() callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

.. _modules-event-connection:

``connectionStateChange.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered when the device connection state changes, use forge.is.connection.connected() and forge.is.connection.wifi() to test new connection state.

This event will also be fired once during app startup, as soon as we determine the connection status.

.. js:function:: event.connectionStateChange.addListener(callback, error)

    :param function() callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``messagePushed.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered when a push notification is received both while the application is running or if the application is launched via that notification.

Currently available as part of our :ref:`integration with Parse <partner-parse>`.

.. js:function:: event.messagePushed.addListener(callback, error)

    :param function(data) callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

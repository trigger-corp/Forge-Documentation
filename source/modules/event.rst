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

``backPressed.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android**

Triggered when the back button is pressed on an Android device.

.. js:function:: event.backPressed.addListener(callback, error)

    :param function(closeApplication) callback: callback invoked when back button is pressed, the first argument is a function which if called will close the application.
    :param function(content) error: called with details of any error which may occur

``backPressed.preventDefault``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android**

Prevents the default action when the back button is pressed from the point this is called onwards, allowing the app to handle the event itself using ``backPressed.addListener``.

.. js:function:: event.backPressed.preventDefault(success, error)

    :param function() success: invoked when no errors occur
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

``appPaused.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered when the app loses focus and moves into the background. At this point what can be executed varies by platform:

* Android: Any javascript can be run, but timers may not be fired until the app is resumed, this prevents unnecessary battery usage by the app.
* iOS: A short amount of time is given for execution, it is generally best to assume that callbacks and timers may not fire until the app is resumed.
* Windows Phone: Any javascript will be executed only when the app resumes.

You should also not assume that an app that is paused will be resumed, the app may be killed at this point by the user or device without ever being resumed.

.. js:function:: event.appPaused.addListener(callback, error)

    :param function(data) callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``appResumed.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered when the app is resumed from a previous paused state.

.. js:function:: event.appResumed.addListener(callback, error)

    :param function(data) callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur
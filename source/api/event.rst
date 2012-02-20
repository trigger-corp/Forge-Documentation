.. _api-event:

Events: ``forge.event``
================================================================================

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
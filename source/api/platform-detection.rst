.. _api-platform-detection:

Platform Detection: ``forge.is``
=========================================================================
Forge allows you to build cross-platform mobile apps and browser extensions from the same code.
Sometimes it may be necessary to do a specific action based on the platform that is running the code.
The following methods allow you to determine what platform that is.

``mobile``
-------------------------------------------------------------------------
.. js:function:: is.mobile()

    :return boolean: Returns true if running on a mobile device

``desktop``
-------------------------------------------------------------------------
.. js:function:: is.desktop()

    :return boolean: Returns true if running on a desktop/laptop computer
 
``android``
-------------------------------------------------------------------------
.. js:function:: is.android()

    :return boolean: Returns true if running on an Android device

``ios``
-------------------------------------------------------------------------
.. js:function:: is.ios()

    :return boolean: Returns true if running on an IOS device

``chrome``
-------------------------------------------------------------------------
.. js:function:: is.chrome()

    :return boolean: Returns true if running on Chrome browser

``firefox``
-------------------------------------------------------------------------
.. js:function:: is.firefox()

    :return boolean: Returns true if running on Firefox browser

``safari``
-------------------------------------------------------------------------
.. js:function:: is.safari()

    :return boolean: Returns true if running on Safari browser

``ie``
-------------------------------------------------------------------------
.. js:function:: is.ie()

    :return boolean: Returns true if running on IE browser

``orientation``
---------------
**Platforms: Mobile**

``portrait``
~~~~~~~~~~~~
.. js:function:: is.orientation.portrait()

    :return boolean: Returns true if a mobile device has a portrait orientation

``landscape``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. js:function:: is.orientation.landscape()

    :return boolean: Returns true if a mobile device has a landscape orientation

.. _api-topbar:

Native top bar: ``forge.topbar``
================================================================================

The ``topbar`` module displays a fixed native header bar in mobile apps and provides a Javascript API to modify it at runtime.

Config
------

The ``topbar`` module must be enabled in config.json as follows:

.. parsed-literal::
    {
        "modules": {
            "topbar": true
        }
    }

API
---

``setTitle``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Set the title displayed in the top bar.

.. js:function:: topbar.setTitle(title, success, error)

    :param string title: Title to be displayed
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``addButton``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Add a button with an icon to the top bar. The first parameter is an object containing a ``icon`` property.

On iOS the first paramater may also contain a ``position`` property, set to ``left`` or ``right`` determining the location of the button. As well as a ``text`` property, which will define text to be shown in place of an icon for the button.

Example::

   forge.topbar.addButton({
     icon: "search.png",
     text: "Search",
     position: "left"
   }, function () {
     alert("Search pressed");
   });

.. js:function:: topbar.addButton(params, callback, error)

    :param object params: Button options, must contain an ``icon`` and optionally ``position`` and ``text``
    :param function() callback: callback to be invoked each time the button is pressed
    :param function(content) error: called with details of any error which may occur

``removeButtons``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Remove currently added buttons from the top bar.

.. js:function:: topbar.removeButtons(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``homePressed.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android**

Triggered when the home button on the top bar is pressed on an Android device

.. js:function:: topbar.homePressed.addListener(callback, error)

    :param function() callback: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur
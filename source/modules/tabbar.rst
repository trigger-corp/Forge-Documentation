.. _modules-tabbar:

``tabbar``: Native tab bar
================================================================================

The ``tabbar`` module shows a fixed footer as part of your app which can show multiple "tab" buttons, these buttons can be selected by the user or activated by Javascript.

Config
------

The ``tabbar`` module must be enabled in config.json as follows:

.. parsed-literal::
    {
        "modules": {
            "tabbar": true
        }
    }

API
---

``setTint``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Set a colour to tint the tabbar with, in effect the tabbar will become this colour with a gradient effect applied.

.. js:function:: tabbar.setTint(color, success, error)

    :param array color: an array of four integers in the range [0,255]
                  that make up the RGBA color of the badge.
                  For example, opaque red is [255, 0, 0, 255].
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``setActiveTint``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Set a colour to tint active tabbar item with.

.. js:function:: tabbar.setActiveTint(color, success, error)

    :param array color: an array of four integers in the range [0,255]
                  that make up the RGBA color of the badge.
                  For example, opaque red is [255, 0, 0, 255].
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``addButton``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Add a button with an ``icon`` and ``text`` to the tabbar. The first parameter is an object of options for the button, which can include:

- ``icon`` (required): This sets the icon which will be shown on the tab, only the alpha channel of the icon will be used with the color being replaced for a consistent style.
- ``text`` (required): This sets the text which will appear below the icon on the tab.
- ``index`` (recommended): This sets the order of the button to be added, not setting this will result in the order of the tabs not being fixed.

When adding a button the success callback will be called with a button object. This object has methods to allow you to interact with the button as follows:

- ``button.remove(success, error)``: Remove the button
- ``button.setActive(success, error)``: Mark the button as selected, without calling this and before the user clicks on one of the buttons no button will be marked active.
- ``button.onPressed.addListener(callback, error)``: Add a callback to handle when the button is pressed

Example::

   forge.tabbar.addButton({
     icon: "search.png",
     text: "Search",
     index: 0
   }, function (button) {
     button.setActive();
     button.onPressed.addListener(function () {
       alert("Search");
     });
   });

.. js:function:: tabbar.addButton(params, success, error)

    :param object params: Button options, must contain an ``icon``, ``text`` and optionally ``index``
    :param function(button) success: called with the button object.
    :param function(content) error: called with details of any error which may occur

``removeButtons``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Remove all buttons from the tabbar.

.. js:function:: tabbar.removeButtons(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur
	

``setInactive``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Unselect any currently active tab, leaving the tabbar with no tabs selected.

.. js:function:: tabbar.setInactive(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur
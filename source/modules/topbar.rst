.. _modules-topbar:

``topbar``: Native top bar
==========================

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

``setTitleImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Set the title displayed in the top bar to an image.

.. js:function:: topbar.setTitleImage(image, success, error)

    :param string image: Path to image to be displayed in topbar.
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``setTint``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Set a colour to tint the topbar with, in effect the topbar will become this colour with a gradient effect applied.

.. js:function:: topbar.setTint(color, success, error)

    :param array color: an array of four integers in the range [0,255]
                  that make up the RGBA color of the badge.
                  For example, opaque red is [255, 0, 0, 255].
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``addButton``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Add a button with an icon to the top bar. The first parameter is an object describing the button with the following properties:

- ``icon``: An icon to be shown on the button.
- ``text``: Text to be shown on the button, either ``text`` or ``icon`` must be set.
- ``type``: Create a special type of button, the only option currently is ``"back"`` which means the button will cause the webview to go back when pressed.
- ``style``: Use a predefined style for the button, currently this can only be ``"done"`` which will style a positive action. This may not work if a tint is set for the topbar.
- ``position``: The position to display the button, either ``left`` or ``right``. If not specified the first free space will be used.
- ``tint``: The color of the button, defined as an array similar to ``setTint``.

Example::

   forge.topbar.addButton({
     text: "Search",
     position: "left"
   }, function () {
     alert("Search pressed");
   });

.. js:function:: topbar.addButton(params, callback, error)

    :param object params: Button options, must contain at least ``icon`` or ``text``
    :param function() callback: callback to be invoked each time the button is pressed
    :param function(content) error: called with details of any error which may occur

``removeButtons``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Remove currently added buttons from the top bar.

.. js:function:: topbar.removeButtons(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur
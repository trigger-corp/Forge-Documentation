.. _modules-topbar:

``topbar``: Native top bar
==========================

The ``topbar`` module displays a fixed native header bar in mobile apps and provides a Javascript API to modify it at runtime.

To get an idea of how these headers can look, see our blog post, `How to build hybrid mobile apps combining native UI components with HTML5 <http://trigger.io/cross-platform-application-development-blog/2012/04/30/how-to-build-hybrid-mobile-apps-combining-native-ui-components-with-html5/>`_.

Config
------

The ``topbar`` module must be enabled in config.json as follows:

.. parsed-literal::
    {
        "modules": {
            "topbar": true
        }
    }

Style Guidlines
----------------

The ``setTitleImage`` method and ``icon`` option in the ``addButton`` method allow you to specify images within the topbar element. These guidelines may help you to make them look good across devices:

   * The title image will be scaled down (but not up) to fit the height of the topbar exactly. This means any padding should be included in the image, and the image should be at least 100px high.
   * The button icons will also be scaled down (but not up) to fit the height of the button precisely. The width of the button is the width of the icon (or text) plus a small amount of padding. We'd recommend button icons are at least 64px high to make sure they always fill the button.
   * The total width of the title and buttons is not checked by Forge, so its up to you to test everything fits, We'd recommend leaving spare space to make sure devices with unexpected screen ratios don't overlap.


API
---

``show``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Shows the topbar. The topbar is shown by default and will only be hidden if you call ``topbar.hide()``.

.. js:function:: topbar.show(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``hide``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Hides the topbar.

.. js:function:: topbar.hide(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

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
- ``style``: Use a predefined style for the button, currently this can either be ``"done"`` which will style a positive action (which may be overriden by ``tint``), or ``"back"`` to show a back arrow style button on iOS.
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

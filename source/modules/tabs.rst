.. _modules-tabs:

``tabs``: Tabs Management
================================================================================

Tabs management provides functionality specific to tabs.

Config
------

The ``tabs`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "tabs": true
        }
    }

API
---

.. _modules-tabs-open:

``open``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

Opens a new tab with the specified url with an option to retain focus on the calling tab.

On mobile this will display a :ref:`modal view <forge-modal>` and the success callback will be called with an object containing a url and optionally a userClosed boolean property.

.. js:function:: tabs.open(url, [keepFocus,] success, error)

    :param string url: The URL to open in the new tab
    :param boolean keepFocus: (optional) If true keeps the current tab focused
    :param function(object) success: callback to be invoked when no errors occurs
    :param function(content) error: called with details of any error which may occur

.. _modules-tabs-openWithOptions:

``openWithOptions``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

As ``open`` but takes an object with the following parameters:

Required:

- ``url``: Required URL to open

Browser only:

- ``keepFocus``: Whether or not to keep focus on the current page.

Mobile only:

- ``pattern``: Pattern to close the modal view, see :ref:`modal views <forge-modal>` for more detail.
- ``title``: Title of the modal view.
- ``tint``: Colour to tint the top bar of the modal view. An array of four integers in the range [0,255] that make up the RGBA color. For example, opaque red is [255, 0, 0, 255].
- ``buttonText``: Text to show in the button to close the modal view.
- ``buttonIcon``: Icon to show in the button to close the modal view, if ``buttonIcon`` is specified ``buttonText`` will be ignored.
- ``buttonTint``: Colour to tint the button of the top bar in the modal view.

Example::

  forge.tabs.openWithOptions({
    url: 'http://my.server.com/login/',
    pattern: 'http://my.server.com/loggedin/*',
    title: 'Login Page'
  }, function (data) {
    forge.logging.log(data.url);
  });

.. js:function:: tabs.openWithOptions(options, success, error)

    :param object options: Object containing url and optional properties.
    :param function(object) success: callback to be invoked when no errors occurs
    :param function(content) error: called with details of any error which may occur

``closeCurrent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

**Restrictions: Only available inside a page (not from a background script)**

Close the tab which makes the call.

.. js:function:: tabs.closeCurrent(error)

    :param function(content) error: called with details of any error which may occur

Permissions
-----------

On Chrome this module will add the ``tabs`` permission to your app, users will be prompted to accept this when they install your app.

.. _modules-button:

``button``: Toolbar button
================================================================================
**Platforms: Browser**

Config
------

The ``button`` configuration controls the appearance and function of toolbar icons in the browsers. With this directive, you can specify a HTML file which will be displayed when the button is clicked, a default button icon as well as platform-specific icons.

.. parsed-literal::
    {
        "modules": {
            "button": {
                ":ref:`default_popup <field-default_popup>`": "popup.html",
                ":ref:`default_title <field-default-title>`": "Button Title",
                ":ref:`default_icon <field-default_icon>`": "my-default-icon.ico",
                ":ref:`default_icons <field-default_icons>`": {
                    "firefox": "my-icon-for-firefox.ico"
                }
            }
        }
    }


.. _field-default_popup:

.. _field-default-title:

.. _field-default_icon:

.. _field-default_icons:

* ``default_popup`` should refer to a local HTML file, included in your app, which will be displayed after the button is clicked; for more information, see :ref:`part I of the tutorial <tutorials-weather-tutorial-1-setting-up-the-UI>`
* ``default_title`` this will show as the tooltip text when users hover over the toolbar button. It is a required field for IE.
* ``default_icon`` should refer to a local image file, included in your app, to be used as the button icon
* ``default_icons`` allows you to override the ``default_icon`` icon, one platform at a time: the object keys should be one or more of ``chrome``, ``firefox``, ``safari`` or ``ie``

.. important:: Internet Explorer requires you to override the ``default_icon`` with a 16x16 bitmap in .ico format.

API
---

Adding and manipulating a toolbar button near the browser's address bar.

``setIcon``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets the icon for the toolbar button.

.. js:function:: button.setIcon(url, success, error)

    :param string url: the URL of the icon
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``setURL``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets the path to the HTML page that should be opened when the toolbar button is clicked.

.. js:function:: button.setUrl(url, success, error)

    :param string url: relative URL to the HTML to set as the toolbar button popup
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``onClicked.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets a function to be executed when the toolbar button is clicked.

.. js:function:: button.onClicked.addListener(callback)

    :param function() callback: function to be executed when the toolbar button is clicked.

``setBadge``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only (Not supported on Internet Explorer)**

Sets a number to appear as a notification badge on the toolbar button.

.. js:function:: button.setBadge(number, success, error)

    :param number number: number to display as badge
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``setBadgeBackgroundColor``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only (Not supported on Safari or Internet Explorer)**

Sets the background color for the badge.

.. js:function:: button.setBadgeBackgroundColor(color, success, error)

    :param array color: an array of four integers in the range [0,255]
                  that make up the RGBA color of the badge.
                  For example, opaque red is [255, 0, 0, 255].
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``setTitle``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Set the tooltip text for a toolbar button.

.. js:function:: button.setTitle(title, success, error)

    :param string title: title text to set as the toolbar tooltip
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur
    

.. _api-button:

Toolbar button: ``forge.button``
================================================================================

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
**Platforms: Browser only**

Sets a number to appear as a notification badge on the toolbar button.

.. js:function:: button.setBadge(number, success, error)

    :param number number: number to display as badge
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``setBadgeBackgroundColor``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only (Not supported on Safari)**

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
    
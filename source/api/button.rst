.. _api-button:

Toolbar button: ``forge.button``
================================================================================

Adding and manipulating a toolbar button near the browser's address bar.

``setIcon``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets the icon for the toolbar button.

.. js:function:: button.setIcon(url)

    :param string url: the URL of the icon
    :param function success: callback to be invoked when no errors occur
    :param function error: callback to be invoked when an error occurs

``setURL``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets the path to the HTML page that should be opened when the toolbar button is clicked

.. js:function:: button.setUrl(url)

    :param string url: relative URL to the HTML to set as the toolbar button popup
    :param function success: callback to be invoked when no errors occur
    :param function error: callback to be invoked when an error occurs

``onClicked.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets a function to be executed when the toolbar button is clicked

.. js:function:: button.onClicked.addListener(fn)

    :param function fn: function to be invoked

``setBadge``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets a number to appear as a notification badge on the toolbar button.

.. js:function:: button.setBadge(number, success, error)

    :param long number: number to display as badge
    :param function success: callback to be invoked when no errors occur
    :param function error: callback to be invoked when an error occurs

``setBadgeBackgroundColor``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only (Not supported on Safari)**

Sets the background color for the badge.

.. js:function:: button.setBadgeBackgroundColor(color, success, error)

    :param array color: an array of four integers in the range [0,255]
    			  that make up the RGBA color of the badge.
    			  For example, opaque red is [255, 0, 0, 255].
    :param function success: callback to be invoked when no errors occur
    :param function error: callback to be invoked when an error occurs
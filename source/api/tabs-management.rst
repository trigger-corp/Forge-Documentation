.. _tabs-management:

Tabs Management: ``forge.tabs``
================================================================================

Tabs management provides functionality specific to tabs

``open``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: tabs.open(url, [keepFocus,] success, error)

    :param string url: The URL to open in the new tab
    :param boolean keepFocus: (optional) If true keeps the current tab focused
    :param function success: callback to be invoked when no errors occurs
    :param function error: callback to be invoked when an error occurs

Opens a new tab with the specified url with an option to retain focus on the calling tab

``closeCurrent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

**Restrictions: Only available inside a page (not from a background script)**

.. js:function:: tabs.closeCurrent()

Close the tab which makes the call.
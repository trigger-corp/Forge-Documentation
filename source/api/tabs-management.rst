.. _tabs-management:

Tabs Management: ``forge.tabs``
================================================================================

Tabs management provides functionality specific to tabs.

``open``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

Opens a new tab with the specified url with an option to retain focus on the calling tab.

On mobile this will display a :ref:`modal view <forge-modal>`.

.. js:function:: tabs.open(url, [keepFocus,] success, error)

    :param string url: The URL to open in the new tab
    :param boolean keepFocus: (optional) If true keeps the current tab focused
    :param function() success: callback to be invoked when no errors occurs
    :param function(content) error: called with details of any error which may occur

``closeCurrent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

**Restrictions: Only available inside a page (not from a background script)**

Close the tab which makes the call.

.. js:function:: tabs.closeCurrent(error)

    :param function(content) error: called with details of any error which may occur

.. _tabs-management:

Tabs Management: ``forge.tabs``
================================================================================

Tabs management provides functionality specific to tabs.

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

``openWithOptions``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

As ``open`` but takes an object of parameters, additionally accepts a match pattern on mobile (see :ref:`modal views <forge-modal>` for more detail).

.. js:function:: tabs.openWithOptions(options, success, error)

    :param object options: Object containing url and optionally keepFocus and pattern properties.
    :param function(object) success: callback to be invoked when no errors occurs
    :param function(content) error: called with details of any error which may occur

Example::

  forge.tabs.openWithOptions({
    url: 'http://my.server.com/login/',
    pattern: 'http://my.server.com/loggedin/*'
  }, function (data) {
    forge.logging.log(data.url);
  });

``closeCurrent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

**Restrictions: Only available inside a page (not from a background script)**

Close the tab which makes the call.

.. js:function:: tabs.closeCurrent(error)

    :param function(content) error: called with details of any error which may occur

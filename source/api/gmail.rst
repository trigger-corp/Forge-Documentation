.. _api-gmail:

Gmail library: ``forge.gmail``
================================================================================

This library makes it easy to create a browser extension to interact with Gmail. It is a useful alternative to creating Gmail gadgets.

To access the Gmail library, add the following to the libs array of your ``config.json`` file::

    "libs": { "gmail":{} },

The WebMynd Forge Gmail library allows you to interact with the following elements of the Gmail composition pane:

.. image:: /_static/gmail/gmail.png


Reference:

#. :ref:`forge.gmail.getToolbar <api-gmail-getToolbar>`
#. :ref:`forge.gmail.getActivePane <api-gmail-getActivePane>`
#. :ref:`forge.gmail.getTo <api-gmail-getTo>`
#. :ref:`forge.gmail.getCC <api-gmail-getCC>`
#. :ref:`forge.gmail.getBCC <api-gmail-getBCC>`
#. :ref:`forge.gmail.getSubject <api-gmail-getSubject>`
#. :ref:`forge.gmail.getComposeDoc <api-gmail-getComposeDoc>`
#. :ref:`forge.gmail.createLinkInComposePane <api-gmail-createLinkInComposePane>`

**Platforms: Chrome only**

.. _api-gmail-injectCSS:

``injectCSS``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Inserts a given stylesheet to the Gmail page. Referencing the stylesheet through ``manifest.json`` will not be recognized by Gmail. Note that if referring to a relative URL for the stylesheet, use :ref:`forge.tools.getURL <miscellaneous>` to resolve the name to a fully-qualified local or remote resource before passing into the function.

.. js:function:: gmail.injectCSS(url)

    :param string url: the URL of the stylesheet
    :param function success: success callback function
    :param function error: error callback function, usually because stylesheet has already been added

.. _api-gmail-pollForComposePane:

``pollForComposePane``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Polls the page and calls a function when it detects that user is in a composition pane, either through 'Compose New Mail' or 'Reply'/'Forward'.

.. js:function:: gmail.pollForComposePane(loadFn, continuous)

    :param function loadFn: function to call once when compose pane is detected and active

.. _api-gmail-getActivePane:

``getActivePane``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Returns the body element of the active Gmail pane. This is useful for using jQuery selectors to get certain elements on the page.

.. js:function:: gmail.getActivePane()

.. _api-gmail-getToolbar:

``getToolbar``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Returns the top toolbar container of the active Gmail pane. This is useful for using jQuery selectors to get certain elements on the page.

.. js:function:: gmail.getToolbar()

.. _api-gmail-getComposeDoc:

``getComposeDoc``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Returns the Gmail composition pane. This is useful for using jQuery selectors to get certain elements on the composition page.

.. js:function:: gmail.getComposeDoc()

.. _api-gmail-getEmailAddress:

``getEmailAddress``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Gets the e-mail address of the user currently logged in. If the user has multiple e-mail address to the account, it will retrieve the selected e-mail in the composition pane.

.. js:function:: gmail.getEmailAddress()

.. _api-gmail-getTo:

``getTo``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrieves the 'to' input element of the composition pane.

To change the 'to' input element, use::

    forge.gmail.getTo().val("example@webmynd.com");

.. js:function:: gmail.getTo()

.. _api-gmail-getCC:

``getCC``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrieves the 'CC' input element of the composition pane.

To change the 'CC' input element, use::

    forge.gmail.getCC().val("example@webmynd.com");

.. js:function:: gmail.getCC()

.. _api-gmail-getBCC:

``getBCC``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrieves the 'BCC' input element of the composition pane.

To change the 'BCC' input element, use::

    forge.gmail.getBCC().val("example@webmynd.com");

.. js:function:: gmail.getBCC()

.. _api-gmail-getSubject:

``getSubject``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Retrieves the 'Subject' input element of the composition pane.

.. js:function:: gmail.getSubject()

.. _api-gmail-createLinkInComposePane:

``createLinkInComposePane``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Creates a link in the composition pane, either as a button along the 'Send', 'Save', 'Discard' row, or a text link among 'Attach a File' and 'Insert: Invitation'.

.. js:function:: gmail.createLinkInComposePane(options, clickFn, text)

    :param object options: settings for link (see below)
    :param function clickFn: function to call on click
    :param string text: text to display as the link  

Currently supported options:
 * type: ``"button"``, ``"link"`` (default)
 * position: ``"first"``, ``"last"`` (default)

.. image:: /_static/gmail/createLink.png

Example #1::

    forge.gmail.createLinkInComposePane(
        { "type":"button", "position":"first"},
        function(){ alert ("click!")},
        "Save to Database"
    );

Example #2::

    forge.gmail.createLinkInComposePane(
        { "type":"link", "position":"last" },
        function(){ alert ("click!")},
        "Save to Database"
    );
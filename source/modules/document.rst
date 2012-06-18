.. _modules-document:

``document``: Document utility functions
========================================

Internet Explorer features a number of inconsistencies with some common document operations, these methods allow you to work around these problems in a platform-independent manner.

API
---
``reload``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser Only**

.. js:function:: document.reload()

Internet Explorer's implementation of document.reload() only refreshes the static content of a page. This method will reload a page and force all scripts to be re-evaluated as well.


``location``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: document.location(success, error)

  :param function(location) success: callback to be invoked when no errors occurs
  :param function(content) error: called with details of any error which may occur

Internet Explorer versions 9 and later aborts page loading with a permission denied message if the document location is accessed from within an iframe. This function provides a workaround which functions correctly under all browsers.

Error object properties:
 * ``statusCode``: Status code returned from the server.
 * ``content``: Content returned from the server (if available).

Example::

  forge.document.location(function(location) {
      forge.logging.log(location.href);
    }, function(error) {
      alert('Failed to get document location: '+error.message);
    }
  });


.. _miscellaneous:

Miscellaneous tools: ``forge.tools``
--------------------------------------------------------------------------------

``UUID``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

A `UUID <http://en.wikipedia.org/wiki/Uuid>`_ is a globally unique token; when represented as a string, they look something like ``18ADF182-7B12-4FA1-AF0B-6032108C0AE8``. Forge already uses UUIDs internally to ensure your extension doesn't conflict with others; this method returns a new UUID for you to use as a unique token.

.. note:: This function is synchronous and returns a value rather than taking a callback.

.. js:function:: tools.UUID()

  :returns: a string representation of the UUID

``getURL``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

Resolve this name to a fully-qualified local or remote resource

.. js:function:: tools.getURL(name, callback, error)

    :param string name: unqualified resource name, e.g. ``my/resource.html``
    :param function(url) callback: will be invoked with the URL as its only parameter
    :param function(content) error: called with details of any error which may occur

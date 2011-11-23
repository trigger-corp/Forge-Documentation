.. _cross-domain:

Cross-domain requests: ``forge.request``
================================================================================

Normal in-page JavaScript is only able to make HTTP requests to the same server as one hosting the current web page. These methods allow you to work around this restriction.

.. note:: For security reasons, you must specify the remote URLs you will send requests to in the ``permissions`` array of your JSON configuration file.

    This array, like the ``patterns`` array, should contain `Match Patterns <http://code.google.com/chrome/extensions/match_patterns.html>`_ to match the remote URLs you want to interact with.

    To protect your users, make these match patterns as restrictive as possible.

``get``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: request.get(url, callback, error)

    :param string url: the URL to GET
    :param function callback: called with the retrieved content body as the only argument
    :param function error: callback to be invoked when an error occurs

The callback function *callback* is invoked with the content body of the requested URL as a string.
As it is limited to ``GET`` requests and lacks the more advanced options of *forge.request.ajax*, it's recommended that *forge.request.get* is only used in very simple scenarios.

``ajax``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: request.ajax(xhrOptions)

  :param object xhrOptions: jQuery-style parameters to control the request

This function is closer to the `jQuery.ajax <http://api.jquery.com/jQuery.ajax/>`_ method than *forge.request.get*. However, the full range of jQuery options are **not supported** for this method, due to the structure of browser and mobile apps.

Also, note that the ``error`` and ``success`` callbacks are **not** passed the jQuery XHR object.

Currently supported options:
 * accepts
 * cache
 * contentType
 * data
 * dataType
 * error
 * password
 * success
 * timeout
 * type
 * url
 * username
 * files (Android only, see :ref:`forge.file <api-file>`)

Example::

  window.forge.ajax({
    type: 'POST',
    url: 'http://my.server.com/update/,
    data: {x: 1, y: "2"},
    dataType: 'json',
    success: function(data, status) {
      alert('Updated x to '+json.x);
    },
    error: function(status, errorThrown) {
      alert('Failed to update x: '+errorThrown);
    }
  });
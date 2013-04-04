.. _modules-request:

``request``: Cross-domain requests
==================================

Normal in-page JavaScript is only able to make HTTP requests to the same server as one hosting the current web page. These methods allow you to work around this restriction.

Config
------

.. note:: For security reasons, you must specify the remote URLs you will send requests to in the ``permissions`` array of your JSON configuration file.

    This array, like the ``patterns`` array, should contain `Match Patterns <http://code.google.com/chrome/extensions/match_patterns.html>`_ to match the remote URLs you want to interact with.

    To protect your users, make these match patterns as restrictive as possible.

.. parsed-literal:: 
    {
        "modules": {
            "request": {
                "permissions": ["https://trigger.io/\*"]
            }
        }
    }

API
---
``get``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: request.get(url, callback, error)

    :param string url: the URL to GET
    :param function(content) callback: called with the retrieved content body as the only argument
    :param function(content) error: called with details of any error which may occur

The callback function *callback* is invoked with the content body of the requested URL. JSON-encoded content will automatically be parsed into a JavaScript object.

As it is limited to ``GET`` requests and lacks the more advanced options of *forge.request.ajax*, it's recommended that *forge.request.get* is only used in very simple scenarios.

.. _request_ajax:

``ajax``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: request.ajax(options)

  :param object options: jQuery-style parameters to control the request

.. note:: unlike jQuery, we expect the URL for the the request to be passed
    into the options hash, *not* as a positional parameter

This function is closer to the `jQuery.ajax
<http://api.jquery.com/jQuery.ajax/>`_ method than *forge.request.get*.
However, the full range of jQuery options are **not supported** for this
method, due to the structure of browser and mobile apps.

Also, note that the ``error`` and ``success`` callbacks are **not** passed a
jQuery XHR object.

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
 * files (Mobile only, see :ref:`forge.file <modules-file>`)
 * fileUploadMethod
 * headers

Error object properties:
 * ``statusCode``: Status code returned from the server.
 * ``content``: Content returned from the server (if available).

Error values (see :ref:`error callback docs <forge-features-api-error>` for more detail):
 * ``type``: ``"UNAVAILABLE"``
 * ``subtype``: ``"NO_INTERNET_CONNECTION"`` No internet connection is currently available (on iOS it is required you inform the user of this if it impacts their current experience).

Example::

  forge.request.ajax({
    type: 'POST',
    url: 'http://my.server.com/update/',
    data: {x: 1, y: "2"},
    dataType: 'json',
    headers: {
      'X-Header-Name': 'header value',
    },
    success: function(data) {
      alert('Updated x to '+data.x);
    },
    error: function(error) {
      alert('Failed to update x: '+error.message);
    }
  });

You can control the name of uploaded files by setting the ``name`` attribute,
e.g.::

  myFile.name = 'name_of_input';
  forge.request.ajax({
    type: 'POST',
    url: 'http://my.server.com/upload/',
    files: [myFile],
    success: function(data) {
      alert('Uploaded file as '+myFile.name);
    },
    error: function(error) {
      alert('Failed to upload file: '+error.message);
    }
  });

If you need to POST an image as the whole request body, use
``fileUploadMethod``. E.g.::

  forge.request.ajax({
    type: 'POST',
    url: 'http://my.server.com/upload_image/',
    fileUploadMethod: "raw",
    success: function(data) {
      alert('Uploaded image');
    }
  });

In this example, the ``Content-Type`` header will be set to ``image/jpeg`` and
the POST body will consist of just the image data with no extra encoding. This
is useful in conjunction with services like `Parse
<https://www.parse.com/tutorials/saving-images>`_.

Permissions
-----------

On Chrome this module will any of the `Match Patterns <http://code.google.com/chrome/extensions/match_patterns.html>`_ you specify to your app, users will be prompted to accept this when they install your app.

.. _api-file:

File access: ``forge.file``
================================================================================

Selecting and using files on the users filesystem.

Notes
~~~~~

- File objects are simple Javascript objects which contain both a ``uri`` and ``name``, they can be serialised using JSON.stringify and safely stored in Forge preferences.
- The ``uri`` parameter can often be used to directly load certain types of files in HTML, for example an image selected using file.getImage() will return a ``uri`` which can be using in an ``<img>`` tag directly.
- Files can be uploaded by including them as an array in ``request.ajax()``. For example if ``myFile1`` and ``myFile2`` where images returned by ``file.getImage()``:

::

    forge.request.ajax({
        url: "http://example.com/file_upload",
        files: [myFile1, myFile2]
    });

``getImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android only**

Returns a file object for a image selected by the user from their phone gallery or taken using their camera.

.. js:function:: file.getImage(success[, error])

    :param function success: callback to be invoked when no errors occur, first argument is the returned file.
    :param function error: callback to be invoked when an error occurs

``base64``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android only**

Returns the base64 value for a files content.

.. js:function:: file.base64(file, success[, error])

    :param file file: the file object to load data from.
    :param function success: callback to be invoked when no errors occur, first argument is the returned file.
    :param function error: callback to be invoked when an error occurs
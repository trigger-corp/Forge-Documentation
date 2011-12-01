.. _api-file:

File access: ``forge.file``
================================================================================

Selecting and using files on the users filesystem.

Notes
~~~~~

- File objects are simple Javascript objects which contain both a ``uri`` and ``name``, they can be serialised using JSON.stringify and safely stored in Forge preferences.
- The ``uri`` parameter can be used directly on some platforms, this is not recommended, instead use one of the provided helper functions such as ``forge.file.imageURL``.
- Files can be uploaded by including them as an array in ``request.ajax()``. For example if ``myFile1`` and ``myFile2`` were images returned by ``file.getImage()``:

::

    forge.request.ajax({
        url: "http://example.com/file_upload",
        files: [myFile1, myFile2]
    });

``getImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns a file object for a image selected by the user from their phone gallery or (if possible on the device) taken using their camera. If an image is taken using their camera it will be saved in the default photo album on the device.

Returned files will be accessible to the app as long as they exist on the device.

.. js:function:: file.getImage(success, error)

    :param function(file) success: callback to be invoked when no errors occur, first argument is the returned file.
    :param function(content) error: called with details of any error which may occur

``isFile``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns true or false based on whether a given object is a file object and points to an existing file on the current device.

.. js:function:: file.isFile(file, success, error)

    :param file file: the file object to check.
    :param function(isFile) success: callback to be invoked when no errors occur, first argument a boolean value.
    :param function(content) error: called with details of any error which may occur

``isImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns true or false based on whether a given object is a file object, points to an existing file on the current device and the file is an image. If attempting to access an image from a previously saved file object it is recommended you use this method to check it still exists first.

.. js:function:: file.isImage(file, success, error)

    :param file file: the file object to check.
    :param function(isImage) success: callback to be invoked when no errors occur, first argument a boolean value.
    :param function(content) error: called with details of any error which may occur

``imageURL``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns a URL which can be used to display an image. Optionally takes a properties object which height and/or width can be set.

This is the recommended way of displaying an image captured from the device. On iOS devices this will return a ``data`` URI with the image encoded as a base64 string, this can be very large for large images. It is therefore highly recommended to set a maximum width and height for the image, based on how you wish to display it. On Android the height and width properties will not be used but the URL returned allows direct access to the image from the webpage so even a full sized image will load quickly, it is however important to also set the height and width of the image when you display it in your html.

Not setting a width and height property will cause iOS apps to become slow and potentially run out of memory.

.. js:function:: file.imageURL(file,[ properties,] success, error)

    :param file file: the file object to load data from.
    :param object properties: an object containing option settings for this method, in this case ``height`` and/or ``width``.
    :param function(url) success: callback to be invoked when no errors occur, first argument is the image URL.
    :param function(content) error: called with details of any error which may occur

``imageBase64``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns the base64 encoded data for an image, with the option to set a maximum height and/or width.

.. js:function:: file.imageBase64(file,[ properties,] success, error)

    :param file file: the file object to load data from.
    :param object properties: an object containing option settings for this method, in this case ``height`` and/or ``width``.
    :param function(base64String) success: callback to be invoked when no errors occur.
    :param function(content) error: called with details of any error which may occur

``base64``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns the base64 value for a files content.

.. js:function:: file.base64(file, success, error)

    :param file file: the file object to load data from.
    :param function(base64String) success: callback to be invoked when no errors occur.
    :param function(content) error: called with details of any error which may occur
.. _api-file:

File and Camera access: ``forge.file``
================================================================================

The file API allows storage of files on the local system as well as capturing images with the camera or selecting them from the users saved photos.

Notes
~~~~~

- File objects are simple Javascript objects which contain at least a ``uri``. They can be serialised using JSON.stringify and safely stored in Forge preferences.
- The ``uri`` parameter can be used directly on some platforms. This is not recommended - instead use one of the provided helper functions such as ``forge.file.URL``.
- Image orientation is automatically handled where possible, if a camera photo contains rotation information it will be correctly rotated before it is displayed or uploaded.
- Files can be uploaded by including them as an array in ``request.ajax()``. For example if ``myFile1`` and ``myFile2`` were images returned by ``file.getImage()``:

::

    forge.request.ajax({
        url: "http://example.com/file_upload",
        files: [myFile1, myFile2]
    });

.. note:: For more information about how to cache remote files in your app, see :ref:`forge-cache`.

``getImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns a file object for a image selected by the user from their photo gallery or (if possible on the device) taken using their camera. If an image is taken using their camera it will be saved in the default photo album on the device.

Images will be stored at their full resolution but resized when displayed or uploaded using the height and width parameters given as the maximum size. Not setting a width and height property can cause apps to become slow and potentially run out of memory.

Returned files will be accessible to the app as long as they exist on the device.

.. js:function:: file.getImage([params, ]success, error)

    :param object params: object optionally containing a height and or width parameter which images will be resized to ensure they are no larger than.
    :param function(file) success: callback to be invoked when no errors occur (argument is the returned file)
    :param function(content) error: called with details of any error which may occur

``cacheURL``
~~~~~~~~~~~~
**Platforms: Mobile**

Downloads a file at a specified URL and returns a file object which can be used for later access. Useful for caching remote resources such as images which can then be accessed directly from the local filesystem at a later date.

Cached files may be removed at any time by the operating system, and it is highly recommended you use the ``isFile`` method to check a cached file is still available before using it.

.. js:function:: file.cachedURL(url, success, error)

    :param string url: URL of file to cache.
    :param function(file) success: callback to be invoked when no errors occur (argument is the returned file)
    :param function(content) error: called with details of any error which may occur

``isFile``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns true or false based on whether a given object is a file object and points to an existing file on the current device.

.. js:function:: file.isFile(file, success, error)

    :param file file: the file object to check
    :param function(isFile) success: callback to be invoked when no errors occur (argument is a boolean value).
    :param function(content) error: called with details of any error which may occur

``URL``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns a URL which can be used to display an image. Height and width will be limited by the values given when originally selecting the image.

.. js:function:: file.imageURL(file, success, error)

    :param file file: the file object to load data from
    :param function(url) success: callback to be invoked when no errors occur, first argument is the image URL
    :param function(content) error: called with details of any error which may occur

``base64``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns the base64 value for a files content.

.. js:function:: file.base64(file, success, error)

    :param file file: the file object to load data from
    :param function(base64String) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``delete``
~~~~~~~~~~
**Platforms: Mobile**

Delete a file from the local filesystem, will work for cached files but not images stored in the users photo gallery.

.. js:function:: file.delete(file, success, error)

    :param file file: the file object to delete
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``clearCache``
~~~~~~~~~~~~~~
**Platforms: Mobile**

Deletes all files currently saved in the local cache.

.. js:function:: file.clearCache(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

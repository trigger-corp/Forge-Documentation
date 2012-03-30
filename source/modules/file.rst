.. _modules-file:

``file``: File and Camera access
================================

The file API allows storage of files on the local system as well as capturing images with the camera or selecting them from the users saved photos.

Notes
-----

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

Config
------

The ``file`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "file": true
        }
    }

API
---

``getImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns a file object for a image selected by the user from their photo gallery or (if possible on the device) taken using their camera. 

The optional parameters can contain any combination of the following:

- ``width``: The maximum height of the image when used, if the returned image is larger than this it will be automatically resized before display. The stored image will not be resized.
- ``height``: As ``width`` but sets a maximum height, both ``height`` and ``width`` can be set.
- ``source``: By default the user will be prompted to use the camera or select an image from the photo gallery, if you want to limit this choice you can set this to ``"camera"`` or ``"gallery"``.
- ``saveLocation``: By default camera photos will be saved to the device photo album, with this setting they can be forced to be saved within your application by using ``"file"``.

Returned files will be accessible to the app as long as they exist on the device.

.. js:function:: file.getImage([params, ]success, error)

    :param object params: object optional parameters.
    :param function(file) success: callback to be invoked when no errors occur (argument is the returned file)
    :param function(content) error: called with details of any error which may occur

``getLocal``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns a file object for a file included in the ``src`` folder of your app

.. js:function:: file.getLocal(path, success, error)

    :param string path: Path to the file, i.e. ``"images/home.png"``.
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

.. js:function:: file.URL(file, success, error)

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

``string``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Returns the string value for a files content.

.. js:function:: file.string(file, success, error)

    :param file file: the file object to load data from
    :param function(string) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``remove``
~~~~~~~~~~
**Platforms: Mobile**

Delete a file from the local filesystem, will work for cached files but not images stored in the users photo gallery.

.. js:function:: file.remove(file, success, error)

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

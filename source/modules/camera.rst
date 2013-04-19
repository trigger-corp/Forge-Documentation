.. _modules-camera:

``camera``: Foreground camera
=============================

Notes
-----

- This module can be used as a drop in replacement for ``file.getImage`` on Android. Unlike :ref:`modules-file`, this module will display the camera as part of your app. This means the user will not have the option to select an image from the gallery, or perform advanced options such as zooming or changing other camera settings. However, on low memory devices this can be a more reliable method of capturing a photo.
- This module is only available on Android, on iOS the ``file`` module will perform a similar function.
- This module uses file objects: it is recommended you process them using the :ref:`modules-file` module.

Config
------

The ``camera`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "camera": true
        }
    }

API
---

``getImage``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Android**

Returns a file object for a image taken using their camera. Images are always saved in your app's "pictures" directory. The file object can be handled using the :ref:`modules-file` module.

The optional parameters can contain any combination of the following:

- ``width``: The maximum height of the image when used, if the returned image is larger than this it will be automatically resized before display. The stored image will not be resized.
- ``height``: As ``width`` but sets a maximum height, both ``height`` and ``width`` can be set.

Returned files will be accessible to the app as long as they exist on the device.

.. js:function:: camera.getImage([params, ]success, error)

    :param object params: object optional parameters.
    :param function(file) success: callback to be invoked when no errors occur (argument is the returned file)
    :param function(content) error: called with details of any error which may occur

Permissions
-----------

On Android this module will add the ``WRITE_EXTERNAL_STORAGE`` and ``CAMERA`` permissions to your app, users will be prompted to accept this when they install your app.
.. _modules-box:

``box``: Upload and Download files with your Box account
======================================================================

The ``forge.box`` APIs allow basic interaction with the `Box <https://www.box.com/>`_ content sharing site.

Box only provide an iOS SDK at the moment, so this module is only available on iOS.

Before you can use this module, you will need to have a Box API key, which you can get here: https://www.box.com/developers/services/edit/

Config
---------------------------------------

The ``box`` module must be enabled in your App Config, and you'll need to provide your API key too:

.. parsed-literal::
    {
        "modules": {
            "box": {
            	"api_key": "8sm2hpmkl2p50do2iyy3d870vk51nryn"
            }
        }
    }

API
---

``box.login``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: iOS**

Open a modal authentication dialog for the user to enter their Box login details.

If the user previously selected "Keep me logged in" while authenticating (and
you haven't called ``box.logout``), the existing authenticated session will be
used - the user will not be prompted to login.

.. note:: If you consistently get a "Wrong username/password" error before you've had a chance to enter your login details, you may have entered your API key incorrectly. This is a known bug in the Box SDK.

.. js:function:: box.login(success, error)

``box.logout``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: iOS**

Immediately log out the current user, so that they will need to re-enter their authentication details next time you call ``box.login``.

.. js:function:: box.logout(success, error)

    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``box.upload``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: iOS**

Upload the supplied file to your Box account.

Currently, only uploading to the root of your Box folder is supported.

.. js:function:: box.upload(fileName, file, success, error)

    :param string fileName: the name we should use for the file when it is in
        box, e.g. "sunset.jpg"
    :param file file: a file object as returned by
        :ref:`file.getImage <modules-file>`
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may
        occur

``box.download``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: iOS**

Download a user-selected file.

A modal file-picker view is shown, which starts the download when the
accessory button is pressed.

.. js:function:: box.download(success, error)

    :param function(file) success: callback to be invoked when no errors occur.
        ``file`` includes various metadata about the file, as well as a ``uri``
        attribute
    :param function(content) error: called with details of any error which may
        occur

Example Usage
------------------------------------------------------------

This code snippet forces a user to login to Box, captures an image from
the device camera,  uploads it to Box, then prompts the user to download a 
file and displays it as an image::

    forge.box.logout(function () {
        forge.box.login(uploadImage, function (err) {
            forge.logging.error("login failed: "+JSON.stringify(err));
        });
    });

    function uploadImage () {
        forge.file.getImage({source: "camera", width: "200px"}, function (file) {
            forge.logging.info("uploading...");
            forge.box.upload('Trigger Image '+Date.now()+".jpg", file, downloadImage);
        });
    }

    function downloadImage () {
        forge.logging.info("downloading...");
        forge.box.download(function (res) {
            forge.logging.info("file metadata: "+JSON.stringify(res));
            document.querySelector('img').setAttribute('src', res.uri);
        });
    }

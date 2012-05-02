.. _modules-media:

``media``: Media file playback
==============================

Config
------

The ``media`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "media": true
        }
    }

API
---

``videoPlay``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Play a video at a URL fullscreen on the device.

.. note:: Allow users to select or capture videos using their device you may use the :ref:`file module<modules-file>`.

.. js:function:: media.videoPlay(url, success, error)

    :param string url: URL to video.
    :param function(file) success: callback to be invoked when no errors occur (argument is the returned file)
    :param function(content) error: called with details of any error which may occur
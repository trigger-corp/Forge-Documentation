.. _modules-media:

``media``: Media file playback
==============================

Config
------

The ``media`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "media": {
            	"enable_background_audio": true
            }
        }
    }

* ``enable_background_audio``: If this is true then audio players will continue to play even when the app is running in the background.

API
---

``videoPlay``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Play a video at a URL fullscreen on the device.

.. note:: Allow users to select or capture videos using their device you may use the :ref:`file module<modules-file>`.

.. js:function:: media.videoPlay(url, success, error)

    :param string url: URL to video.
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``createAudioPlayer``
~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Create a audio player object from a media file which can then be used to play the audio.

The audio player object returned in the success callback has the following methods, all of which take success and error callbacks in the same manner as other Forge methods:

* ``player.play(success, error)``: Begin (or resume) playing the audio file.
* ``player.pause(success, error)``: Pause the playback of the file.
* ``player.stop(success, error)``: Stop the playback of the file and release the audio system.
* ``player.duration(success, error)``: Calls the success callback with the duration of the audio in seconds.
* ``player.seek(seekTo, success, error)``: Seek to the given time (in seconds) in the audio file, if the file is playing it will continue to play after seeking.

.. warning:: For ``player.duration`` and ``player.seek`` to work properly on Android, use 128kb/s constant bit-rate MP3 files.

Example::

  forge.file.getLocal("music.mp3", function (file) {
    forge.media.createAudioPlayer(file, function (player) {
      player.play();
    });
  });

.. js:function:: media.createAudioPlayer(file, success, error)

    :param string file: File object created using forge.file methods representing audio object.
    :param function(player) success: callback to be invoked when player has been created
    :param function(content) error: called with details of any error which may occur
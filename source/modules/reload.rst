.. _modules-reload:

``reload``: Push updates to deployed apps
=========================================

Config
------

The ``reload`` module must be enabled in ``config.json``, once the ``reload`` module is enabled you will be able to push updates to any builds of your app from that point.

.. parsed-literal::
    {
        "modules": {
            "reload": true
        }
    }

API
---

In order to use ``reload`` no API calls are required, however some apps may which to use the following API methods to force updates at a users request, or switch the user to an alternate streams.

``updateAvailable``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Gives ``true`` or ``false`` depending on whether there is a ``reload`` update available to be downloaded.

.. js:function:: reload.updateAvailable(success, error)

    :param function(update_available) success: Called with whether or not an update is available.
    :param function(content) error: called with details of any error which may occur

``update``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Forces the application to check for, and if available download a ``reload`` update. The update will then be applied if ``applyNow`` is called, or if not the next time the app is closed or loses focus.

.. js:function:: reload.update(success, error)

    :param function() success: Called when an update is ready to be applied
    :param function(content) error: called with details of any error which may occur

``applyNow``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Immediately applies a downloaded ``reload`` update if one is ready to be applied. This means any assets that make up the app may be changed from the point of the ``success`` callback firing. In this situation it is up to the app to refresh/reload any resources that may have changed.

.. js:function:: reload.applyNow(success, error)

    :param function() success: Update has been applied
    :param function(content) error: called with details of any error which may occur

``switchStream``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Switches the ``reload`` stream the app will download updates from.

.. js:function:: reload.switchStream(stream_name, success, error)

    :param function() success: Stream switched
    :param function(content) error: called with details of any error which may occur

Update process
--------------

The ``reload`` update process has several parts. First, it must be determined if an update is available, and if it is available it needs to be downloaded. Once an update has been downloaded it has to be applied, this means making the new files available to the app. If the app is running while an update is applied then there may need to be additional code in the app to make use of the updated files.

The following things will cause ``reload`` to download new update files if available:

* A call to ``forge.reload.update()``.
* On all platforms new files will be downloaded shortly after the app is launched.
* On Android and iOS new files will also be downloaded when the app loses focus but is running in the background.
* On Android new files will also be downloaded when the app exits.

Assuming an update has been fully downloaded and is ready to apply the following things will replace the apps assets files with the new update:

* A call to ``forge.reload.applyNow()``.
* On all platforms when the app is relaunched (i.e. when it has been quit and opened again).
* On iOS and Android when the app is restored from the background.

If updates are applied during launching or restoring an app ``index.html`` will be reloaded with the new update files. If ``forge.reload.applyNow()`` is called manually then it is up to the app to perform any refresh required.

Notes
-----

* Updates may take some time if the user is on a slow network, however several things are done to improve this, only changed files are downloaded in an update, and if an update is interrupted part way through it will resume where it left off next time it is started.
* On iOS updates are given 10 minutes to download each time the app is paused as this is the maximum amount of background processing time available on iOS. If an update is interrupted it will resume where it left off on the next attempt.
* Only one update is downloaded at a time, if an update is waiting to be applied any future updates will not be downloaded until it has been applied to the app. This should never be a problem for real users but may be confusing during testing.
* When testing the easiest way to cause an update is to leave the app by pressing the home button on the device, wait a few seconds (or look at the log output to see when the reload update is complete), and reopen the app to see the update applied.
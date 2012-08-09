.. _release-notes:

Release Notes
===============================================================================

This file contains information about new features and capabilities of Forge versions, along with migration information for how to upgrade from one level to another.

In your ``config.json`` file, you can use a major version (like ``v1.3``), which means you will receive rolling updates and fixes, or you can use a minor version (like ``v1.3.2``), which will only be updated with critical fixes and security patches.

To see the minor version used to create a particular build, look in ``.template/platform_version.txt`` in your app directory (``.template`` sits alongside ``src``).

.. _release-notes-v1.4:

v1.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Android
* iOS
* Windows Phone
* Chrome
* Firefox
* Safari
* Internet Explorer
* Web

Changes from v1.3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The v1.4 major version changes the format of config.json slightly, putting the
``orientations`` configuration inside a new ``display`` module.

In addition, due to internal changes in how Forge apps work, you will no longer
be able to make cross-domain requests without using the ``forge.request``
module or `CORS <http://www.w3.org/TR/cors/>`_.

.. _upgrade-1.4:

Upgrade Instructions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To upgrade from v1.3 to v1.4, we provide a command which automates the process
of updating your ``config.json`` file.

If you're using the command-line tools, just run ``forge migrate``: we will
create a backup of your current ``config.json`` file in ``src/config.json.bak``.

.. note:: v1.4 requires iPad retina launchimage configuration: see :ref:`the
    module documentation <modules-launchimage>`.

You should also check your code is not attempting to make cross-domain XHRs:
either use ``forge.request`` instead (recommended), or CORS if you prefer.

v1.4.8
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 8th August 2012**

Bug fixes:

- relative resource paths in CSS files on iOS
- make AVD creation more resilient to failure
- handle lack of JRE more gracefully
- force IE popups to the foreground

v1.4.7
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 7th August 2012**

Bug fixes:

- playback of locally bundled media files fixed on iOS
- loading locally bundled resources in modal views fixed on iOS
- fixed incompatibility between iOS contact module and MS Exchange

v1.4.6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 2nd August 2012**

Features:

- Facebook authentication details returned as parameter to facebook.authorize

Bug fixes:

- ``minimum_version`` configuration on Android was causing build problems for some
- remove dependency on Express 2.5.0 for web target
- remove default orientation configuration and fix Android "any" mode

v1.4.5
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 1st August 2012**

Bug fixes:

- ensure focus events work properly for popup windows on IE

v1.4.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 31st July 2012**

Bug fixes:

- fix internal generateQueryString method on IE

v1.4.3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 26th July 2012**

Bug fixes:

- creating modal dialogs was broken on some older versions of Android

v1.4.2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 24th July 2012**

Bug fixes:

- enable use of modal views immediately after app launch on iOS
- modules are fully disabled by default, unless explicitly enabled

v1.4.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 20th July 2012**

Features:

- support retina scaled images for iPad
- integration with native Facebook SDKs
- use ``enableHighAccuracy`` in iOS geolocation API

Bug fixes:

- topbar and tabbar buttons are correctly re-added after app is closed on Android
- network activity indicator properly cleared after closing iOS modal views

v1.4.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 17th July 2012**

Features:

- :ref:`Reload <modules-reload>`
- lifecycle events (appPaused and appResumed :ref:`docs <modules-event>`)
- barcode scanning module: :ref:`modules-barcode`
- use Chrome manifest version 2 (see :ref:`modules-requirements`)
- fullscreen support (:ref:`modules-display`)

.. _release-notes-v1.3:

v1.3
-------------------------------------------------------------------------------

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Android
* iOS
* Windows Phone
* Chrome
* Firefox
* Safari
* Internet Explorer
* Web

Changes from v1.2
~~~~~~~~~~~~~~~~~

The v1.3 platform release changes the format of config.json to put most optional configuration into separate modules, this allows Forge to provide more features without having them all enabled for every app.

By default all of the features from v1.2 will be enabled, but these can be disabled if not required. Disabled modules allow the Forge generation process to remove code from your app, making it smaller. Modules also define the permissions your app will required, so disabled unused modules will reduce the permissions users are prompted for when installing your app.

.. _upgrade-1.3:

Upgrade Instructions
~~~~~~~~~~~~~~~~~~~~

To upgrade from v1.2 to v1.3 your ``config.json`` file needs to be updated, this can be done automatically by running ``forge migrate`` with the command line tools, or choosing to migrate from Trigger Toolkit.

The migration process will automatically update your ``config.json`` file to v1.3, if for any reason it doesn't work a backup of your ``config.json`` file will be saved as ``config.json.bak``.

v1.3.23
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 20 July 2012**

Features:

- migration script to upgrade to v1.4

v1.3.22
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 18th July 2012**

Bug fixes:

- launchimage on iPad is correctly sized

v1.3.21
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 12th July 2012**

Features:

- network activity spinner / progress bar shown while loading modal views

Bug fixes:

- connectionStateChanged callbacks are fired at least once
- request.ajax response contains the body data for non-200 status codes on Android

v1.3.20
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 12th July 2012**

Bug fixes:

- re-enable running Firefox automatically
- clean up some extra files produced by new Android SDK

v1.3.19
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 3rd July 2012**

Bug fixes:

- forge.prefs fix for Internet Explorer

v1.3.18
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 3rd July 2012**

Features:

- allow ad-hoc builds to be created on iOS

Bug fixes:

- update to latest Parse Android SDK for push notifications fixes
- panel sizing fix for Firefox

v1.3.17
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 22nd June 2012**

Bug fixes:

- a Python fix which makes us less incompatible with 2.6 - note 2.7 is still
  the only officially supported Python version!
- Windows Phone IE does not support setZeroTimeout

v1.3.16
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 18th June 2012**

Bug fixes:

- "no such file or directory" during Android tasks on some Linux setups
- Node.js directory locking issue on Windows
- lots of Trigger Toolkit UI tweaks and fixes
- allow for running Forge builds on non-root mount point

v1.3.15
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 11th June 2012**

Features:

- better Q & A system for Trigger Toolkit
- build for iOS on Windows: http://trigger.io/cross-platform-application-development-blog/2012/05/31/work-on-what-you-want-week-at-trigger-io/
- iframes are allowed on iOS now - embed media players, buttons and so on

Bug fixes:

- ``about:blank`` caused app to crash in iOS simulator
- logcat process were left hanging after runs

v1.3.14
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 30th May 2012**

Features:

- can install apps to SD card on Android

Bug fixes:

- default value for file character encoding guess
- handle non-ASCII command line parameters
- playVideo callback is fired after video finishes and focus returns
- mailto: links handled properly in modal views

v1.3.13
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 22nd May 2012**

Features:

- show / hide topbar and tabbar programmatically
- specify minimum version of iOS and Android
- complete ``forge.file`` support on Windows Phone 7
- in-app purchase support
- updated Firefox SDK

v1.3.12
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 17th May 2012**

Features:

- ``.template/platform_version.txt`` created as part of build process
- button popups on IE are moved and resized intelligently

Bug fixes:

- index not required for tabbar.addButton
- large number of tabbar buttons handled properly
- callbacks firefox after tabbar and topbar buttons added

v1.3.11
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 15th May 2012**

Features:

- disable icon glossiness on iOS (:ref:`docs <modules-icons>`)
- ``file.getLocal`` and ``file.string`` support in non-mobile platforms (:ref:`docs <modules-file>`)
- `Catalyst <http://trigger.io/catalyst/>`_ shows waiting message until debugger has connected

Bug fixes:

- run app on Android emulator, when emulator has been started automatically
- prebuild hooks are found and run correctly

v1.3.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 10th May 2012**

Features:

- full video support on Android and iOS
- topbar module on Windows Phone

Bug fixes:

- callbacks sometimes not invoked after tabbar.addButton
- window.forge initialisation sometimes got stuck in a loop
- NullPointerException sometimes occurring when using console.log on Android
- prevent BroadcastReceiver intent leak on Android
- prevent console windows popping up during Toolkit builds

v1.3.9
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 8th May 2012**

Features:

- greatly improved error messages and status codes for failed HTTP requests on Android

v1.3.8
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 7th May 2012**

Bug fixes:

- handle change in status codes returned by Heroku API

v1.3.7
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 6th May 2012**

Features:

- Windows Phone 7 support: partial

Bug fixes:

- ensure iOS permission dialog shown on main thread: was sometimes not visible
- fix segfault which occurred in some situations showing camera on iPhone running v5.1

v1.3.6
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 3rd May 2012**

Bug fixes:

- character encoding guessing now deals with empty files
- ensure connection change event is fired soon after app startup
- callbacks are properly fired for camera usage (iOS) and modal views (Android)
- launch images on Android

v1.3.5
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 2nd May 2012**

Features:

- connection status information in :ref:`forge.is.connection<modules-is>`, as well as :ref:`connection state change events<modules-event>`
- `Web SQL <http://www.w3.org/TR/webdatabase/>`_ support

.. warning:: Web SQL is not supported in all browsers or on all devices: http://caniuse.com/#search=websql

v1.3.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 29th April 2012**

Bug fixes:

- Parse push notifications were not recieved on Android in some situations

v1.3.3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 27th April 2012**

Features:

- styling for :ref:`modal views on mobile<modules-tabs-openWithOptions>`
- better incremental builds: faster development cycle in normal conditions

Bug fixes:

- authentication loop occurring in some situations when deploying code to Heroku
- users cancelling out of iPad gallery now fires the error callback
- support for nested JavaScript objects sent through forge.request.ajax
- incorrect keystore password produces clearer error message

v1.3.2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 19th April 2012**

Bug fixes:

- handle :ref:`the native top bar<modules-topbar>` not being styleable on older iPhones
- disable troublesome Windows Phone builds temporarily

v1.3.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 17th April 2012**

Features:

- :ref:`pre-build hooks<tools-hooks>`
- re-use server-side builds, improving ``forge build`` performance

Bug fixes:

- correct usage of ``homepage``, ``update_url``, ``author`` and ``icons`` entries from your config.json in various browser extension manifests
- quitting Android 2.1 app with the back button was causing app crash
- push notifications with Parse on iOS were not enabled properly
- process suspended while looking for Android device on Linux
- better handling of location permission denied after image capture on iOS

v1.3.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 5th April 2012**

Features:

- :ref:`button module <modules-button>` on IE
- ``getLocal`` function in :ref:`file module <modules-file>`
- native bar at bottom of app: :ref:`tabbar module <modules-tabbar>`
- ask for the minimum set of required permissions on Android

.. _release-notes-v1.2:

v1.2
-------------------------------------------------------------------------------

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* Firefox
* iOS
* Web

v1.2.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 27th April 2012**

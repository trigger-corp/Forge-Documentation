.. _release-notes:

Release Notes
===============================================================================

This file contains information about new features and capabilities of Forge versions, along with migration information for how to upgrade from one level to another.

In your ``config.json`` file, you can use a major version (like ``v1.3``), which means you will receive rolling updates and fixes, or you can use a minor version (like ``v1.3.2``), which will only be updated with critical fixes and security patches.

v1.3 (*current version*)
-------------------------------------------------------------------------------

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* iOS
* Firefox
* Safari
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

v1.2 (*previous version*)
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

.. _release-notes:

Release Notes
===============================================================================

This file contains information about new features and capabilities of Forge versions, along with migration information for how to upgrade from one level to another.

In your ``config.json`` file, you can use a major version (like ``v1.3``), which means you will receive rolling updates and fixes, or you can use a minor version (like ``v1.3.2``), which will only be updated with critical fixes and security patches.

To see the minor version used to create a particular build, look in ``.template/platform_version.txt`` in your app directory (``.template`` sits alongside ``src``).

.. _release-notes-v1.4:

v1.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Supported Targets
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

.. note:: v1.4 requires iPad retina launchimage configuration: see
    :ref:`the module documentation <modules-launchimage>`.

You should also check your code is not attempting to make cross-domain XHRs:
either use ``forge.request`` instead (recommended), or CORS if you prefer.

v1.4.36
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 27th March 2013**

Bug fixes:

- re-installing iOS IPAs on top of existing installations caused hangs on launchimage in some situations

v1.4.35
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 20th March 2013**

Features:

- can set minimum required iOS version to be 6.0: :ref:`modules-requirements`
- allow the `web` target Node.js app to be deployed at non-root paths (http://stackoverflow.com/questions/15070765/)

Bug fixes:

- fix crash in API demo (https://github.com/trigger-corp/Forge-API-Demo/issues/7)
- fix playback of video and audio after Reload usage on iOS - note the Gotchas on :ref:`reload`!

v1.4.34
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 12th March 2013**

Bug fixes:

- fix slight inaccuracy when adding calendar events: :ref:`modules-calendar`
- fix race condition where tabbar buttons could be wrongly ordered: :ref:`modules-tabbar`
- fix modal view redirect on older versions of Android (http://stackoverflow.com/questions/15262840/)
- fix NullPointerException in urlhandler module :ref:`modules-urlhandler` (http://stackoverflow.com/questions/13824961/)
- fix cross-device link error (http://stackoverflow.com/questions/11578443/)

v1.4.33
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 6th March 2013**

Bug fixes:

- application of Reload updates was broken on iOS devices

v1.4.32
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 4th March 2013**

Features:

- support for subscription payments on Android: see :ref:`modules-payments`
- support for using the ``forge`` APIs on trusted remote HTML pages: see :ref:`config`

Bug fixes:

- update to Android Parse SDK version 1.1.15 to fix http://stackoverflow.com/questions/14811733/

v1.4.31
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 28th February 2013**

Features:

- new ``installationInfo`` API for Parse, by popular demand: see :ref:`partner-parse`
- pause Reload updates, and receive progress updates: see :ref:`modules-reload`
- create file fixtures when developing native plugins: see :ref:`native_plugins_file_objects`
- update Parse SDK to version 1.1.32

Bug fixes:

- benign stack trace on startup from ``urlhandler`` module
- enhanced date inputs on Android now fire on touchend rather than touchstart (http://stackoverflow.com/questions/14551349/)
- fix ``minimum_version`` requirement for iOS

v1.4.30
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 15th February 2013**

Bug fixes:

- handle Android gallery not including Exif data in photos

v1.4.29
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 30th January 2013**

Bug fixes:

- sensible fallback if image processing fails on Android

v1.4.28
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 30th January 2013**

Bug fixes:

- include ``ForgeFile.h`` in native plugin Inspector projects on iOS

v1.4.27
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 29th January 2013**

Features:

- Exif orientation data is used when displaying or uploading images on Android
- launch IE as original user after extension installation
- prefix plugin projects with name in Eclipse
- update Parse Android SDK to version 1.1.11

Bug fixes:

- ``forge.request`` was interacting badly with Reload in some situations on Android
- fix threading issues in :ref:`barcode <modules-barcode>` and `Catalyst <https://trigger.io/catalyst/>`_
- Parse broadcast channel was broken on Android

v1.4.26
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 17th January 2013**

.. note:: Due to the switch to using Gson, the way to return non-primitive results from native plugins has changed: see :ref:`native_plugins_native_communication`

Features:

- create calendar events with the :ref:`calendar module <modules-calendar>`
- Use Gson for JSON parsing and serialisation for increased performance on Android
- new ``forge.file.saveURL`` API: :ref:`modules-file`

Bug fixes:

- IE activates properly on pages opened with ``target="_blank"``
- Android datepicker activates for ``datetime-local`` inputs
- Android datepicker results are properly zero-padded

v1.4.25
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 14th January 2013**

Bug fixes:

- support for large Android launchimages
- fix for NumberFormatException in Android contacts module
- ``facebook.ui`` result now has same schema as the JavaScript SDK

v1.4.24
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 18th December 2012**

Features:

- you can run the iOS simulator at a specified version with ``simulatorfamily`` and ``simulatorsdk`` - see :ref:`parameters-in-a-file`

Bug fixes:

- Android launchimages are scaled properly on high pixel density screens
- HTTP 401 does not cause NullPointerException on Android when no username and password supplied

v1.4.23
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 7th December 2012**

Features:

- server-side code signing for IE extensions
- Android native date picker fires ``blur`` event when complete
- during development on Windows or Linux, iOS apps are only partially code-signed for performance

Bug fixes:

- fullscreen display didn't work for holo theme Android devices
- Android native date picker follows W3C spec when returning values
- ``facebook.ui`` returns dialog outcome information on iOS

v1.4.22
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 30th November 2012**

Features:

- support for IE 10 extensions

Bug fixes:

- Android native date picker results were off-by-one on the month
- unicode characters in app description caused build failures on some platforms
- running the "web" target repeatedly would cause address in use errors on OS X

v1.4.21
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 21st November 2012**

Features:

- ability to set the background color behind Android launch images (:ref:`docs <modules-launchimage>`)

Bug fixes:

- incorrect data was returned for emails by the contacts API on Android
- handle usage of unavailable APIs more gracefully

v1.4.20
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 7th November 2012**

Features:

- cookies are persisted by default on Android
- Windows Phone builds are now done against the version 8 SDK
- launch image can be hidden manually (:ref:`docs <modules-launchimage>`)
- support for iOS 6.1 beta
- native date / time pickers for Android (:ref:`docs <modules-ui>`)

Bug fixes:

- fix issue where only Google contacts were returned by ``contact.selectAll``
- modal views wouldn't close when user hit back button on Android

v1.4.19
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 29th October 2012**

Features:

- Command-line tools bundled in Toolkit can update the Toolkit install
- native plugins v1 - see :ref:`native_plugins`
- Flurry analytics module: see :ref:`docs <modules-flurry>`
- update to Firefox Addon SDK 1.10
- ability to manually quit the app when the back button is pressed on Android - see :ref:`modules-event`

v1.4.18
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 15th October 2012**

Bug fixes:

- "publish" permissions work properly with new Facebook SDK on iOS 6

v1.4.17
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 12nd October 2012**

Features:

- support for using Linux for iOS builds: :ref:`tools-ios-linux`
- true native back buttons for the topbar module on iOS: :ref:`modules-topbar`
- update to version 3.1.1 of the Facebook SDK for iOS for :ref:`modules-facebook`
- new ``selectAll`` and ``selectById`` methods in :ref:`modules-contact`
- new Facebook API to check authentication status
- support for coloured status bar on iOS 6 (``setTint`` in :ref:`modules-topbar`)
- ability to create and use wireless distribution manifests for iOS :ref:`best-practice-wireless-distribution`

Bug fixes:

- video uploads to Facebook API were failing

v1.4.16
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 1st October 2012**

.. warning:: Due to a bug to do with resource caching in iOS 6, we've been
    forced to remove the ``applyNow`` method from the Reload module.

Features:

- more intelligent diff made during Reload update: faster and less bandwidth consumed
- ability to build for iPad or iPhone/iPod only: :ref:`modules-requirements`
- post-build hooks: :ref:`tools-hooks`
- hooks are passed the currently-building target as first command-line argument
- build and run iOS apps from Linux :ref:`tools-ios-linux`

Bug fixes:

- fix json2.js operation on IE9 running in IE7 compatability mode
- ability to set the same cookie several times in one request on web target
- localStorage and webSql databases are persisted correctly

v1.4.15
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 25th September 2012**

Features:

- register custom URL schemes: :ref:`modules-urlhandler`
- beta of custom native plugins complete :ref:`native_plugins`

Bug fixes:

- non-ASCII characters in some config fields were causing build problems
- can run Firefox extensions automatically on Linux
- Android landscape launchimages properly used
- ``null`` values in multipart/form-data requests are not sent to server

v1.4.14
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 17th September 2012**

.. warning:: To accommodate the iPhone 5, this platform version requires you to
    set the new ``iphone-retina4`` configuration directive in the :ref:`launchimage
    module <modules-launchimage>`.

Features:

- support for iOS 6 and iPhone 5

Bug fixes:

- fixed canvas ``drawImage`` crashing when using external resources

v1.4.13
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 4th September 2012**

Features:

- consider build timestamps while Reloading so new installs don't apply older updates
- add ``node_path`` local configuration option if Node.js is not on your path: :ref:`web-best_practices`
- programmatically control allowed app orientation: :ref:`modules-display`

Bug fixes:

- fix POST encoding of objects in arrays http://stackoverflow.com/questions/12194600/forge-request-ajax-post-data-as-json
- fix iPad landscape-mode launchimage distortion
- IE installer uses configured icon as branding

v1.4.12
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 24th August 2012**

Features:

- option to :ref:`disable hardware acceleration <modules-requirements>` on Ice Cream Sandwich due to some rendering issues in libraries such as KendoUI
- iOS: automatically use distribution developer certificate with distribution provisioning profile and vice versa

Bug fixes:

- updated iOS app install utility for better Mountain Lion support, faster operation and increased reliability
- Forge-based IE extensions can be disabled in IE 9
- initial connectionStateChanged event fired even earlier
- tabbar and topbar buttons aren't duplicated by Reload
- content is zoomable and pannable in Android modal views
- cookies containing double quotes work when using web target with Opera

v1.4.11
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 22nd August 2012**

Bug fixes:

- fix Facebook API regression, where authentication flows didn't return to the app
- fix Express's zlib dependency on Heroku http://stackoverflow.com/questions/11995324/zlib-module-not-playing-nicely-with-web-deployment

v1.4.10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 20th August 2012**

Features:

- can set name of files uploaded through request.ajax
- better Reload download logic to speed up update deployment

Bug fixes:

- fullscreen mode incompatible with orientation limitation on iOS
- unicode characters in app config could cause problems in some situations
- prerendered icons for iOS were broken

v1.4.9
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 13th August 2012**

Features:

- re-use of Reload files already present on iOS device

Bug fixes:

- version number updated properly in IE setup scripts
- resource loading on iOS improved using Reload
- tools.getURL needed adjustment for Reload

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

Supported Targets
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
- ``file.getLocal`` and ``file.string`` support in non-mobile targets (:ref:`docs <modules-file>`)
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

Supported Targets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* Firefox
* iOS
* Web

v1.2.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Released: 27th April 2012**

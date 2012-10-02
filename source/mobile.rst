.. _mobile-index:

Forge and Mobile
=================================================

The following tutorial is intended to get anyone up to speed developing iOS and Android apps using Forge.

This process does not require you to know Objective C, Java or any platform specific API calls.
The only things needed is a basic understanding of HTML and JavaScript.

We're working hard to make Forge the simplest way to make mobile apps. We hope you'll find our guides easy to follow - 
but if you get stuck at any point, just drop us a line on support@trigger.io. We'd love to help!

.. _mobile-getting-started:

This guide will take you through building your first mobile app with Forge. We recommmend reading :ref:`forge-index` first to set up your environment.

Preparing to run mobile apps
-----------------------------

**Goal: Set up development environment**

Forge can be used to generate both iOS and Android apps from a single codebase. We will explain the set up of both platforms so that you can follow the subsequent tutorial with either (or both).

Setting up an iOS environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To build and run iOS apps, you can use a Mac or Windows computer. However, to use the iOS simulator, a Mac is required.

For more information on how to build for iOS from a non-Mac computer, see
:ref:`tools-ios-windows` and our `Build and test your iPhone / iPad app on
Windows
<http://trigger.io/cross-platform-application-development-blog/2012/06/13/new-features-test-iphone-ipad-apps-on-windows-and-linux-embed-media-players-and-widgets-updated-toolkit/>`_
blog post.

To test your app locally you can use the iOS Simulator if you have a Mac. This
is included with XCode, which you can download from
https://developer.apple.com/xcode/. When this is installed, start XCode and
click 'Preferences' from the XCode menu to check the iOS Simulator is listed as
installed under components. If not, you may install it from that window.

Setting up an Android environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to build your app for Android there is a minimum requirement of having Python and Java installed. Both commands should be installed and made available on your path.

If you have setup the command-line tools, you should already have Python 2.7 installed.

In order to run your built app, you'll need an attached phone with debug drivers installed or an active Android emulator device. If you do not set this up yourself, the command line tools will detect this and offer to create an appropriate Android Virtual Device (AVD) for you - simply follow any instructions given to you by the commands.

If you wish to manually manage your Android emulator you can setup the Android SDK location, by clicking on your app from the Your Apps page, then clicking on 'Local config' in the top right.

.. image:: /_static/images/local-config.png

At the command-line, use the ``--android.sdk`` flag when using ``forge run android`` to point to your Android SDK location and run your own emulator AVD. All automatic installation procedures will prompt before making any changes to your system.

.. important:: There is a bug in the Android 2.3 emulator that will render your apps unusable: if you manage your own Android AVD you **must** use an Android 2.2 level AVD.

Hello Mobile
-------------
**Goal: Adding static content**

* After going through the :ref:`forge-index` section you should see a ``src`` directory created inside your app directory.
  This is where all of your app files should be placed
* The ``src`` directory should contain a ``config.json`` file which holds all of the configuration settings for the app. You can also edit this file from inside the Toolkit, by click on your app name in the Your Apps page and then the 'App config' link in the top right.
* Open ``src/index.html`` in your favorite text editor

* You will see the HTML for a default "Hello World" app: you can use this as a starting point for your real app.

.. note:: Forge looks for index.html as the entry point of your application. **This file must be present and the name cannot be changed.**

We can now generate and run the application.
The following sections explain how to build and run the code.

.. _mobile-getting-started-build:
.. _mobile-getting-started-run:

Building and running the code
------------------------------
**Goal: To see your iOS and Android apps running**

You can build and test your app using either the toolkit or the command-line.

.. note:: If you change your HTML, CSS or JavaScript between builds, then they will take just a couple of seconds. If you change the local config (in the ``config.json``) file, a full rebuild will occur which will take longer

Toolkit
~~~~~~~~

From the Your Apps screen, simply click on the app name you wish to build.

You can then click the appropriate link to build and run the app for Android or iOS. You will see the full traceback in the console as the commands are run so you can see progress and any warnings.

.. image:: /_static/images/toolkit-run.png

If you make subsequent code changes that you want to build and test on the same platform, just click 'Run again' at the bottom of the console view in the app run page.

.. image:: /_static/images/toolkit-again.png

Command-line
~~~~~~~~~~~~~

At the command-line you must use two commands ``forge build`` and ``forge run`` to build and test an app. See :ref:`command_line_setup` for the location of the ``forge`` executable for your platform.

To build your app:

* Navigate to your app directory
* Run ``forge build ios`` and ``forge build android`` to create your iOS and Android apps. 
* Whenever the configuration file changes the entire app needs to be rebuilt.
* When the build finishes take a look inside the ``development`` directory and you should see ``android`` and ``ios`` directories

To test your app on iOS:

   * Type ``forge run ios``
   * Apple requires apps to be packaged before deploying to iOS devices (see :ref:`releasing<releasing>` for instructions) so this will launch the simulator 

To test your app on  Android: 

   * Type ``forge run android``
   * To use an Android device, connect it with **USB Debugging** enabled and the appropriate drivers installed
   * If no device is available, we will automatically start the Android emulator

.. image:: /_static/android/weather/images/windows-forge-run-android.png

If something goes wrong take a look at our :ref:`faq`.

Dynamic Hello
--------------
**Goal: Running dynamic JavaScript code and using logging**

Ok, perhaps that wasn't all too impressive - let's add some dynamic functionality next.

* Replace the contents of the ``body`` element in ``index.html`` with::

    <p>Hello World, this is HTML!</p>

* Create the file ``js/default.js`` and change its contents to::

    forge.logging.info('Hello World, this is JavaScript');

* Open ``index.html`` and make sure ``default.js`` is being included::

    <script type="text/javascript" src="js/default.js"></script>

* :ref:`Rebuild<mobile-getting-started-build>` and :ref:`re-run <mobile-getting-started-run>` the application: you should see your "Hello World" message in the app.
* Look at the command prompt/terminal running the code and you should see your "Hello World" log message.

.. important:: Now that you know how to use logging it is highly encouraged to use it frequently for debugging purposes.

Reference app
-------------------
The files in `getting-started.zip <_static/weather/getting-started.zip>`_ represent the code you should have in your src folder at this point.  If you run into any issues this is a good place to look.

Troubleshooting
---------------
Hopefully you've made it this far without any issues, but if there are any problems at this point, see our :ref:`faq`.

What next?
----------------------------------
If everything went well and you're ready to move on to some more fancy things, why not try our
:ref:`Mobile Weather App <tutorials-weather-tutorial-1>` tutorial?

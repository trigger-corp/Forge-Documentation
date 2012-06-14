.. _mobile-index:

Forge and Mobile (iOS and Android)
=================================================

The following tutorial is intended to get anyone up to speed developing iOS and Android apps using Forge.

This process does not require you to know Objective C, Java or any platform specific API calls.
The only things needed is a basic understanding of HTML and JavaScript.

We're working hard to make Forge the simplest way to make mobile apps. We hope you'll find our guides easy to follow - 
but if you get stuck at any point, just drop us a line on support@trigger.io. We'd love to help!

.. _mobile-getting-started:

Mobile Getting Started
~~~~~~~~~~~~~~~~~~~~~~

This guide will take you through building your first mobile app with Forge. We recommmend reading :ref:`forge-index` first to set up your environment.

Preparing to run mobile apps
-----------------------------

**Goal: Set up development environment**

Forge can be used to generate both iOS and Android apps from a single codebase. We will explain the set up of both platforms so that you can follow the subsequent tutorial with either (or both).

Setting up an iOS environment
-----------------------------
To build and run iOS apps, you can use a Mac, Windows or Linux computer. However, to use the iOS simulator, a Mac is required.

For more information on how to build for iOS from a non-Mac computer, see
:ref:`tools-ios-windows` and our `Build and test your iPhone / iPad app on
Windows and Linux
<http://trigger.io/cross-platform-application-development-blog/2012/06/13/new-features-test-iphone-ipad-apps-on-windows-and-linux-embed-media-players-and-widgets-updated-toolkit/>`_
blog post.

To test your app locally you can use the iOS Simulator if you have a Mac. This
is included with XCode, which you can download from
https://developer.apple.com/xcode/. When this is installed, start XCode and
click 'Preferences' from the XCode menu to check the iOS Simulator is listed as
installed under components. If not, you may install it from that window.

We have found some unresponsiveness when apps 'over scroll' in iOS Simulator 5.0 so recommend installing version 4.3 too. This lagging performance is only an issue in the simulator, not in actual devices.

Setting up an Android environment
-----------------------------------
In order to build your app for Android there is a minimum requirement of having Python and Java installed (you should already have Python to run any of the command line tool commands). Both commands should be installed and made available on your path.

In order to run your built app, an attached phone with debug drivers installed or an active Android emulator device are required. If you do not set this up yourself the command line tools will do so automatically - simply follow any instructions given to you by the commands.

If you wish to manually manage your Android emulator you can use the ``--android.sdk`` flag when using ``forge run`` to point to your Android SDK location and run your own emulator AVD. All automatic installation procedures will prompt before making any changes to your system.

.. important:: There is a bug in the Android 2.3 emulator that will render your apps unusable: if you manage your own Android AVD you **must** use an Android 2.2 level AVD.

Hello Mobile
-------------
**Goal: Adding static content**

* After going through the :ref:`forge-index` section you should see a ``src`` directory created inside your app directory.
  This is where all of your app files should be placed
* The ``src`` directory should contain a ``config.json`` file which holds all of the configuration settings for the app
* Open ``index.html``

* You will see the HTML for a default "Hello World" app: you can use this as a starting point for your real app.

.. note:: Forge looks for index.html as the entry point of your application. **This file must be present and the name cannot be changed.**

We can now generate and run the application.
The following sections explain how to build and run the code.

.. _mobile-getting-started-build:

Building the code
-----------------
* Windows users open a command prompt. OSX/Linux users open a terminal.
* Navigate to the directory where you extracted the build tools.
* Windows users run ``go.bat``. OSX/Linux users run ``source go.sh``. This will ensure all dependencies are installed and start the virtual environment.
* Navigate to your app directory (if you followed the :ref:`forge-index` section, this will be ``../demo-app``).
* Run ``forge build`` to create your iOS and Android apps
* Whenever the configuration file changes the entire app needs to be rebuilt.
* When the build finishes take a look inside the ``development`` directory and you should see ``android`` and ``ios`` directories

.. _mobile-getting-started-run:

Running the Code
----------------
**Goal: To see your iOS and Android apps running**

* To test the iOS app type ``forge run ios``
   * Apple requires apps to be packaged before deploying to iOS devices (see :ref:`releasing<releasing>` for instructions) so this will launch the simulator 
* To test the Android app type ``forge run android``
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

* Open the file ``js/default.js`` and change its contents to::

    forge.logging.info('Hello World, this is JavaScript');

* Open ``index.html`` and make sure ``default.js`` is being included::

    <script type="text/javascript" src="js/default.js"></script>

* :ref:`Rebuild<mobile-getting-started-build>` and :ref:`re-run <mobile-getting-started-run>` the application: you should see your "Hello World" message in the app.
* Look at the command prompt/terminal running the code and you should see your "Hello World" log message.

.. important:: Now that you know how to use logging it is highly encouraged to use it frequently for debugging purposes.

Reference app
-------------------
The files in `getting-started.zip <../_static/weather/getting-started.zip>`_ represent the code you should have in your src folder at this point.  If you run into any issues this is a good place to look.

Troubleshooting
---------------
Hopefully you've made it this far without any issues, but if there are any problems at this point, see our :ref:`faq`.

What next?
----------------------------------
If everything went well and you're ready to move on to some more fancy things, why not try our
:ref:`Mobile Weather App <tutorials-weather-tutorial-1>` tutorial?

.. _mobile-getting-started:

Mobile Getting Started
======================

This guide will take you through building your first mobile app with Forge. We recommmend reading :ref:`forge-index` first to set up your environment.

Preparing to run mobile apps
-----------------------------

**Goal: Set up development environment**

Forge can be used to generate both iOS and Android apps from a single codebase. We will explain the set up of both platforms so that you can follow the subsequent tutorial with either (or both).

Setting up an iOS environment
-----------------------------
To test your app locally you will need the iOS Simulator. This is included with XCode, which you can download from https://developer.apple.com/xcode/. When this is installed, start XCode and click 'Preferences' from the XCode menu to check the iOS Simulator is listed as installed under components. If not, you may install it from that window.

We have found some unresponsiveness when apps 'over scroll' in iOS Simulator 5.0 so recommend installing version 4.3 too. This lagging performance is only an issue in the simulator, not in actual devices.

When the simulator starts, you can indicate which SDK version you want to use from the Hardware > Version menu. You can select a device (iPhone or iPad) from the Hardware > Device menu. Both of these options are remembered for the next time you start the simulator.

Setting up an Android environment
-----------------------------------
In order to build your app for Android there is a minimum requirement of having Python and Java installed (you should already have Python to run any of the command line tool commands). Both commands should be installed and made available on your path.

In order to run your built app an attached phone with debug drivers installed or an active Android emulator device are required. If you do not set this up yourself the command line tools will do so automatically - simply follow any instructions given to you by the commands.

If you wish to manually manage your Android emulator you can use the ``--android.sdk`` flag when using ``forge run`` to point to your Android SDK location and run your own emulator AVD. All automatic installation procedures will prompt before making any changes to your system.
   
.. important:: There is a bug in the Android 2.3 emulator that will render your apps unusable: if you manage your own Android AVD you **must** use an Android 2.2 level AVD.

Hello Mobile
-------------
**Goal: Adding static content**

* After going through the :ref:`forge-index` section you should see a ``src`` directory created inside your app directory.
  This is where all of your app files should be placed
* The ``src`` directory should contain a ``config.json`` file which holds all of the configuration settings for the app
* Create a file called ``index.html``

.. note:: Forge looks for index.html as the entry point of your application. **This file must be present and the name cannot be changed.**

* Open ``index.html`` and append the following:

.. code-block:: html

    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
          Hello Mobile!
        </body>
    </html>

That's all it takes! We can now generate and run the application.
The following sections explain how to build and run the code.
If everything goes well you should see the text "Hello Mobile" displayed when the app runs.

.. _mobile-getting-started-build:

Building the code
-----------------
Make sure no Android virtual device is running when you try to build the code or you might see "Cannot create a file when that file already exists" error. For more information click :ref:`here<mobile-troubleshooting-build-fail>`

* Windows users open a command prompt. OSX/Linux users open a terminal.
* Navigate to the directory where you extracted the build tools.
* Windows users run ``go.bat``. OSX/Linux users run ``source go.sh``. This will ensure all dependencies are installed and start the virtual environment.
* Navigate to your app directory (if you followed the :ref:`forge-index` section, this will be ``../demo-app``).
* Run ``forge build`` to create your iOS and Android apps
* Whenever the configuration file changes the entire app needs to be rebuilt.
  The initial build will take longer than regular builds.
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

.. important:: The Android ``adb`` tool that we rely on here is quite unreliable: you may need to detach and re-attach your device for it to be recognised.

.. image:: /_static/android/weather/images/windows-forge-run-android.png

If something goes wrong take a look :ref:`at our troubleshooting instructions <mobile-troubleshooting>`.

Dynamic Hello
--------------
**Goal: Running dynamic JavaScript code and using logging**

Ok, perhaps that wasn't all too impressive - let's add some dynamic functionality next.

* Remove the “Hello Mobile!” text from the body of ``index.html``
* Create a file called ``content.js`` and add the following code::

    function writeGreeting(name){
        forge.logging.info('Hello '+name);
    };
    writeGreeting('Forge user!');

* Open ``index.html`` and add a script tag to reference ``contents.js``:

.. code-block:: html

    <head>
      <script type="text/javascript" src="content.js"></script>
    </head>

* :ref:`Rerun <mobile-getting-started-run>` the application
* Take a look at the command prompt/terminal running the code and you should see the log message from ``writeGreeting``.

.. important:: Now that you know how to use logging it is highly encouraged to use it frequently for debugging purposes.

Reference extension
-------------------
The files in `getting-started.zip <../_static/weather/getting-started.zip>`_ represent the code you should have in your src folder at this point.  If you run into any issues this is a good place to look.

Troubleshooting
---------------
Hopefully you've made it this far without any issues, but if there are any problems at this point

* If you are using the Android emulator make sure you are using Android 2.2 (Android 2.3 on the emulator has a known issue which will cause Forge to fail).
* If you decided to stray from the directions and change the names of files or any of the code
  go back to basics and once the code is functional make any desired changes.
* Make sure you include the script tag inside ``index.html`` to the correct JavaScript file.
* If the documentation is at all unclear or if you're still having issues contact
  support@trigger.io with "Mobile Tutorial" as the subject.

If everything went well and you're ready to move on to some more fancy things, why not try our
:ref:`Mobile Weather App <tutorials-weather-tutorial-1>` tutorial?

.. _android-getting-started:

Getting Started
===============

Preparing to run Android apps
-----------------------------

**Goal: Set up development environment**

Before we start using the Forge Android tools, there is a minimum requirement of having Python and Java installed (you should already have Python to run any of the command line tool commands). Both commands should be installed and made available on your path.

At this point you can simply run the commands as explained below. In order to run your built app an attached phone with debug drivers installed or an active Android emulator device are required. If you do not set this up yourself the command line tools will do so automatically - simply follow any instructions given to you by the commands.

If you wish to manually manage your Android emulator you can use the ``--android.sdk`` flag when using ``forge run`` to point to your Android SDK location and run your own emulator AVD. All automatic installation procedures will prompt before making any changes to your system.
   
.. important:: There is a bug in the Android 2.3 emulator that will render your apps unusable: if you manage your own Android AVD you **must** use an Android 2.2 level AVD.

Hello Android
-------------
**Goal: Adding static content**

* After going through the :ref:`forge-index` section you should see a ``src`` directory created inside your app directory.
  This is where all of your app files should be placed
* The ``src`` directory should contain a ``config.json`` file which holds all of the configuration settings for the app
* Create a file called ``index.html``

.. note:: Forge looks for index.html as the entry point of your Android application. **This file must be present and the name cannot be changed.**

* Open ``index.html`` and append the following:

.. code-block:: html

    <!DOCTYPE html>
    <html>
        <head>
        </head>
        <body>
        Hello Android!
        </body>
    </html>

That's all it takes! We can now generate and run the application.
The following sections explain how to build and run the code.
If everything goes well you should see the text "Hello Android" displayed when the app runs.

.. _android-getting-started-build:

Building the code
-----------------
Make sure no AVD is running when you try to build the code or you might see "Cannot create a file when that file already exists" error.
For more information click :ref:`here<android-weather-troucleshooting-build-fail>`

* Windows users open a command prompt. OSX/Linux users open a terminal.
* Navigate to the directory where you extracted the build tools.
* Windows users run ``go.bat``. OSX/Linux users run ``source go.sh``. This will ensure all dependencies are installed and start the virtual environment.
* Navigate to your app directory (if you followed the :ref:`forge-index` section, this will be ``../demo-app``).
* Run ``forge build``
* Whenever the configuration file changes the entire app needs to be rebuilt.
  The initial build will take longer than regular builds.
* When the build finishes take a look inside the ``development`` directory and you should see an ``android`` directory

.. _android-getting-started-run:

Running the Code
----------------
**Goal: Launching the Emulator and seeing your custom code running**

#. You can run your app on an actual device, or use the Android emulator
   * To use an Android device, connect it with **USB Debugging** enabled and the appropriate drivers installed
   * If no device is available, we will automatically start an Android emulator for you
#. Run ``forge run android``

.. important:: The ``adb`` tool that we rely on here is quite unreliable: you may need to detach and re-attach your device for it to be recognised.

.. image:: /_static/android/weather/images/windows-forge-run-android.png

If something goes wrong take a look :ref:`at our troubleshooting instructions <android-weather-troubleshooting>`.

Dynamic Hello
--------------
**Goal: Running dynamic JavaScript code and using logging**

Ok, perhaps that wasn't all too impressive - let's add some dynamic functionality next.

.. note:: logging currently doesn't work with the iOS emulator. We are fixing this as a high priority.

* Remove the “Hello Android!” text from the body of ``index.html``
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

* :ref:`Rerun <android-getting-started-run>` the application
* Take a look at the command prompt/terminal running the code and you should see the log message from ``writeGreeting``.
* **Important: Now that you know how to use logging it is highly encouraged to use it frequently for debugging purposes**

Reference extension
-------------------
The files in `getting-started.zip <../_static/weather/getting-started.zip>`_ represent the code you should have in your src folder at this point.  If you run into any issues this is a good place to look.

Troubleshooting
---------------
Hopefully you've made it this far without any issues, but if there are any problems at this point

* If you are using the Android emulator make sure you are using Android 2.2, Android 2.3 on the emulator has a known issue which will cause Forge to fail.
* If you decided to stray from the directions and change the names of files or any of the code
  go back to basics and once the code is functional make any desired changes.
* Make sure you include the script tag inside ``index.html`` to the correct JavaScript file.
* If the documentation is at all unclear or if you're still having issues contact
  support@trigger.io with "Android Tutorial" as the subject.

If everything went well and you're ready to move on to some more fancy things you can try writing an
:ref:`Android Weather App <weather-tutorial-1>`.

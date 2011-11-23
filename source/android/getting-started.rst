.. _android-getting-started:

Getting Started
===============

Preparing to run Android apps
-----------------------------

**Goal: Set up development environment**

Before we start using the Forge Android tools, there is a minimum requirement of having python and Java installed (you should already have python to run any of the command line tool commands). Both commands should be installed and made available on your path.

At this point you can simply run the commands as explained below, in order to run your build app an attached phone with debug drivers installed or an active Android emulator device are required. If you do not set this up yourself the command line tools will do so automatically, simply follow any instructions given to you by the commands.

If you wish to manually manage your Android emulator you can use the ``-sdk`` flag when using ``wm-run`` to point to your Android SDK location and run your own emulator AVD, all automatic installation procedures will prompt before making any changes to your system.
   
.. important:: There is a bug in the Android 2.3 emulator that will render your apps unusable: if you manage your own Android AVD you **must** use an Android 2.2 level AVD.

Hello Android
-------------
**Goal: Adding static content**

* After going through the :ref:`forge-index` section you should see a ``src`` directory created.
  This is where all of your app files should be placed
* The ``src`` directory should contain a ``config.json`` file which holds all of the configuration settings for the app
* Create a file called ``index.html``. **Important: WebMynd looks for index.html as the entry point of your Android application.**
  **This file must be present and the name cannot be changed.**

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
Make sure no AVD is running when you try to build the code, else you might see "Cannot create a file when that file already exists" error.
For more information click :ref:`here<android-weather-troucleshooting-build-fail>`

* Windows users open a command prompt. OSX/Linux users open a terminal.
* Navigate to the directory where you extracted the build tools
* Windows users run ``go.bat``. OSX/Linux users run ``source go.sh``. This will ensure all dependencies are installed and start the virtual environment.
* Run ``wm-dev-build``
* Whenever the configuration file changes the entire app needs to be rebuilt.
  The initial build will take longer than regular builds.
  Also when the configuration file has been altered you must be connected to the internet to run the build tool.
* When the build finishes take a look inside the ``development`` directory and you should see an ``android`` directory

.. _android-getting-started-run:

Running the Code
----------------
**Goal: Launching the Emulator and seeing your custom code running**

#. Optionally connect your Android device with **USB Debugging** enabled and the appropriate drivers installed, or start your Android emulator AVD, if you do not do this the tools will prompt you to automatically create and run an AVD.
#. Run ``wm-run android``

   **Note: You can optionally pass a -s flag to specify the location of the Android SDK, this is only required if you installed the Android SDK manually.**

.. image:: /_static/android/weather/images/windows-running-androiddev.png

If something goes wrong take a look :ref:`here <android-weather-troubleshooting>`

Dynamic Hello
--------------
**Goal: Running dynamic JavaScript code and using logging**

Ok perhaps that wasn't all too impressive, let's add some dynamic functionality next.

* Remove the “Hello Android!” text from the body of ``index.html``
* Create a file called ``content.js`` and add the following code::

    function writeGreeting(name){
        window.forge.logging.log('Hello '+name);
    };
    writeGreeting("Sahil");

* Open ``index.html`` and add a script tag to reference ``contents.js``:

.. code-block:: html

    <head>
    <script type="text/javascript" src="content.js"></script>
    </head>

* :ref:`Rerun <android-getting-started-run>` the application
* Take a look at the command prompt/terminal running the code and you should see the greeting
* **Important: Now that you know how to use logging it is highly encouraged to use it frequently for debugging purposes**

Reference extension
-------------------
The files in ``/demo/android/weather/hello android`` folder represent the code you should have at this point.
If you run into any issues this is a good place to look.

Troubleshooting
---------------
Hopefully you've made it this far without any issues, but if there are any problems at this point

* If you are using the Android emulator make sure you are using Android 2.2, Android 2.3 on the emulator has a known issue which will cause Forge to fail.
* If you decided to stray from the directions and change the names of files or any of the code
  go back to basics and once the code is functional make any desired changes.
* Make sure you include the script tag inside ``index.html`` to the correct JavaScript file.
* If the documentation is at all unclear or if you're still having issues contact
  support@webmynd.com with "Android Tutorial" as the subject.

If everything went well and you're ready to move on to some more fancy things you can try writing an
:ref:`Android Weather App <weather-tutorial-1>`.
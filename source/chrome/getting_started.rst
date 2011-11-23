Getting Started
===============

.. _chrome-getting-started:

Hello Chrome
-------------
* After going through the :ref:`forge-index` section you should see a ``src`` directory created.This is where all of your extension files will be placed.
* Inside the folder you should see ``config.json`` which is automatically generated. This file holds configuration settings for your extension.
* Create a file called ``background.js`` inside the ``src`` directory and add the following code::

    window.alert('Hello Chrome');

* This code will run in the :ref:`background context<extension-concept-background>`, but we have to reference it in the configuration file first.
* Open ``config.json`` and add this file to the *background_files* array ::

    "background_files": ["background.js"],

The next sections will explain how to build and load the extension.
If everything goes well you should see an alert pop up with the message "Hello Chrome" when the extension is loaded in Chrome.

.. _chrome-getting-started-build:

Building Chrome Extensions Using Forge
--------------------------------------
* Windows users open a command prompt. OSX/Linux users open terminal.
* Navigate to the directory where you extracted the build tools
* Windows users run ``go.bat``. OSX/Linux users run ``source go.sh``. This will ensure all dependencies are installed and start the virtual environment.
* Run ``wm-dev-build``
* Whenever the configuration file changes the entire extension needs to be rebuilt.
  The initial build will take longer than regular builds.
  Also when the configuration file has been altered you must be connected to the internet to run the build tool.
* When the build finishes take a look inside the ``development`` directory and you should see your generated Chrome extension

.. _chrome-getting-started-load-extension:

Loading Chrome Extensions
--------------------------
* Open the Chrome browser and go to ``chrome:extensions``.
* If **Developer mode** isn't already enabled click the ``[+]`` button at the top right
* Click **Load unpacked extension**
* Navigate to the ``development`` directory which contains the generated extension
* Select the ``chrome`` folder and click **OK**
* You should see 'Hello Chrome' alert window as soon as the extension has loaded.


Now that you're familiar with some basics try going through the :ref:`Weather App tutorial<weather-tutorial-1>`\ .
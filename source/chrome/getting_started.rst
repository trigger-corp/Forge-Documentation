Getting Started
===============

.. _chrome-getting-started:

Hello Chrome
-------------
* After going through the :ref:`forge-index` section you should see a ``src`` directory created. This is where all of your extension files will be placed.
* There will be several files and folders in the src directory: this is a basic "Hello World" app.
* Inside the folder you should see ``config.json`` which is automatically generated. This file holds configuration settings for your extension.
* Open the file called ``background.js`` inside the ``src/js`` directory; you should see something like::

    forge.logging.info("This is executed once per extension/browser launch");

* This code will run in the :ref:`background context<extension-concept-background>`, but only if we reference it in the configuration file first.
* Open ``config.json``: note how we use the :ref:`background <modules-background>` module to use our ``background.js`` file::

    "background": {
        "files": [
            "js/background.js"
        ]
    },

The next sections will explain how to build and load the extension.

.. _chrome-getting-started-build:

Building Chrome Extensions Using Forge
--------------------------------------
* Windows users open a command prompt. OSX/Linux users open terminal.
* Navigate to the directory where you extracted the build tools
* Windows users run ``go.bat``. OSX/Linux users run ``source go.sh``. This will ensure all dependencies are installed and start the virtual environment.
* Run ``forge build``.
* Whenever the configuration file changes the app needs to be rebuilt.
* When the build finishes take a look inside the ``development`` directory and you should see your generated Chrome extension.

.. _chrome-getting-started-load-extension:

Loading Chrome Extensions
--------------------------
* Open the Chrome browser and go to ``chrome:extensions``.
* If **Developer mode** isn't already enabled click the ``[+]`` button at the top right.
* Click **Load unpacked extension**.
* Navigate to the ``development`` directory which contains the generated extension.
* Select the ``chrome`` folder and click **OK**.
* Expand section for your Chrome extension by clicking the ▶
* Click forge.html
* A Chrome debugging window will appear: this is where you can debug your background scripts.
* In the console, you should see your message::
    .. image:: /_static/images/developer-tools.png
* If you see an error, see our :ref:`faq`.

What next?
--------------------------------
Now that you're familiar with some basics try going through the :ref:`Weather App tutorial<tutorials-weather-tutorial-index>`.

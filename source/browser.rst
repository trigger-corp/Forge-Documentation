.. _chrome-index:

Forge and Browser Add-ons
======================================================

The Forge platform enables you to easily and quickly write add-ons that run on Chrome, Firefox, Internet Explorer and Safari. We'll take you through how to :ref:`Get Started <chrome-getting-started>` below, but first lets cover some concepts:

Concepts
--------

Add-ons built on the Forge platform have two main aspects:

#. code to run when the browser is started
#. code to run when a page loads

.. _addon-concept-background:

Code run at startup: "background code"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If your add-on relies on long-running code which is not attached or associated with any particular web page, you should use background code.

This code is loaded once when the browser is open or add-on is loaded/reloaded. It runs until the browser is closed or the add-on is removed. It is good practice to put page independent logic/functionality in the background.

To use background files, you need to use the :ref:`background <modules-background>` module.

.. _addon-concept-content-scripts:

Code run at page load: "content scripts"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If your add-on works with the individual web pages a user sees, you should use content scripts.

For example, an add-on which changes a web page so that any long words are replaced with links to that word in an online dictionary.

To use content scripts, you need to use the :ref:`activations <modules-activations>` module.

.. _addon-concept-popup:

Code run when a button is clicked: "popup code"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You can use the :ref:`button <modules-button>` module to add an icon to the brower toolbar.

The HTML page which may be displayed when a user clicks on this icon can include JavaScript. This JavaScript is executed each time the popup is opened, and is destroyed when the popup is closed; therefore, it is closer conceptually to content scripts than background code.

Getting Started
---------------

.. _chrome-getting-started:

Hello Chrome
~~~~~~~~~~~~

* After going through the :ref:`forge-index` section you should see a ``src`` directory created. This is where all of your add-on files will be placed.
* There will be several files and folders in the src directory: this is a basic "Hello World" app.
* Inside the folder you should see ``config.json`` which is automatically generated. This file holds configuration settings for your add-on. You can edit this from inside the Toolkit by click on your app from the Your Apps page, then the 'Local config' link in the top-right
* Open the file called ``background.js`` inside the ``src/js`` directory; you should see something like::

    forge.logging.info("This is executed once per extension/browser launch");

* This code will run in the :ref:`background context<addon-concept-background>`, but only if we reference it in the configuration file first.
* Open ``config.json``: note how we use the :ref:`background <modules-background>` module to use our ``background.js`` file::

    "background": {
        "files": [
            "js/background.js"
        ]
    },

The next sections will explain how to build and load the add-on.

.. note:: Google calls add-ons on Chrome 'extensions'. They're conceptually the same thing and different platforms have different conventions on naming. When talking about Chrome specifically, we'll use 'extensions'.

.. _chrome-getting-started-build:

Building and testing Chrome extensions using Forge
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To build your Chrome extension using the Toolkit, simple click on the app you wish to build from the Your Apps screen, and then the 'Chrome' link. You will see the full traceback in the console as the commands are run so you can see progress and any warnings.

If you make subsequent code changes that you want to build and test on the same platform, just click 'Run again' at the bottom of the console view to rebuild it.

Using the command-line tools, use the ``forge build`` command. When the build finishes take a look inside the ``development`` directory and you should see your generated Chrome extension.

.. _chrome-getting-started-load-extension:

To test the Chrome extensions:

   * Open the Chrome browser and go to ``chrome:extensions``.
   * If **Developer mode** isn't already enabled click the ``[+]`` button at the top right.
   * Click **Load unpacked extension**.
   * Navigate to the ``development`` directory which contains the generated extension.
   * Select the ``chrome`` folder and click **OK**.
   * Expand section for your Chrome extension by clicking the ?
   * Click forge.html
   * A Chrome debugging window will appear: this is where you can debug your background scripts.
   * In the console, you should see your message:
    .. image:: /_static/images/developer-tools.png

If you see an error, see our :ref:`faq`.

What next?
~~~~~~~~~~
Now that you're familiar with some basics try going through the :ref:`Weather App tutorial<tutorials-weather-tutorial-index>`.

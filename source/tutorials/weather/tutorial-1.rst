.. _tutorials-weather-tutorial-1:

Tutorial Part 1
================

In this tutorial, we will step through building a basic weather app using the Forge tools.

This section of the tutorial will guide you through setting up the display,
creating internal data representation, and doing some basic debugging using logging.

When using this tutorial, you should choose a single platform to follow along with: either iOS, Android, mobile website or Chrome extension.
The code we'll be writing will work on any platform, but the configuration steps are different.

The parts that are specific to a platform will be marked with **(Mobile Only)** or **(Chrome Only)**.

.. contents::
   :backlinks: none

Goal
----
This part of the tutorial is intended to:

* Show how to add project files
* Set up weather forecast data structures
* Familiarize you with developing and running a basic app using Forge

.. _tutorials-weather-tutorial-1-preparation:

Preparation
-----------
* Firstly, if you haven't already done so, go through the :ref:`mobile-getting-started` or :ref:`chrome-getting-started` instructions.
  This will help you set up the basics and teach you how to build and run your code.
* Remove any files in the ``src`` directory except ``config.json``, ``identity.json`` and the ``js`` folders (the remaining files will not be needed for the rest of this tutorial).
* Download `resources.zip <../../_static/weather/resources.zip>`_, which contains images and other resources needed for this tutorial; extract the ``resources`` directory inside the ``src`` directory.
* Create a new javascript file called ``weather.js`` inside the ``src/js`` directory. This file will contain all of the JavaScript code for the rest of the tutorial.
* Create a file called ``index.html`` inside the ``src`` directory. This will be the html page that displays the forecast information.

.. _tutorials-weather-tutorial-1-setting-up-the-UI:

Setting up the UI
-----------------
**Goal: Displaying static content**

Open ``index.html`` in your favorite editor and add the following:

.. code-block:: html

    <!DOCTYPE html>
    <html>
     <head>
      <script type="text/javascript" src="js/weather.js"></script>
     </head>
     <body>
      Weather forecast here.
     </body>
    </html>

Notice the script tag in the head element points to ``weather.js`` file you created earlier.
This file does not need any code at this point.

**(Chrome only)**
For a chrome extension a :ref:`toolbar button<modules-button>` will be added near the browsers address bar which will display ``index.html`` when clicked.
Toolbar buttons can have an image to differentiate them from other extension toolbar buttons.
There is an icon ``sun_19.png`` inside the resources directory which is the correct size and provided specifically for this purpose.

Open ``config.json`` and add the following configuration to the ``modules`` section to set up the toolbar button.

.. important:: JSON requires all key value pairs to be separated by commas.
    Makes sure to place proceeding or trailing commas as appropriate!

::

    "button": {
        "default_popup": "index.html",
        "default_icon": "resources/sun_19.png"
    },

Build and run the code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Instruction on how to build and run a mobile app can be found :ref:`here <mobile-getting-started-build>`.
- Instructions on how to build and load an extension for Chrome can be found :ref:`here<chrome-getting-started-build>`.

On Chrome, a new toolbar icon should be visible!

Create dummy data
-------------------------------------------
**Goal: Set up some dummy data for a weather forecast**

.. _tutorials-weather-tutorial-1-forecast-information:
.. _tutorials-weather-tutorial-1-current-conditions:

First, we will create some dummy data in JSON format - open ``src/js/weather.js`` and paste the following code::

    var forecast = {
        city: "Mountain View, CA",
        forecast_date: "2011-08-09"
    };
    
    var currentConditions = {
        condition: "Clear",
        temp_f: "73",
        humidity: "Humidity: 57%",
        icon: "resources/sunny.gif",
        wind_condition: "Wind: N at 9 mph"
    };

.. _tutorials-weather-tutorial-1-forecast-conditions:

We'll use a helper function to create daily forecast objects::

    var forecastConditionMaker = function(day_of_week, low, high, icon, condition) {
        return {
            day_of_week: day_of_week,
            low: low,
            high: high,
            icon: icon,
            condition: condition
        }
    };

    var tuesdayConditions = forecastConditionMaker("Tue", "58","72", "resources/mostly_sunny.gif","Clear");
    var wednesdayConditions = forecastConditionMaker("Wed", "58", "72", "resources/sunny.gif", "Clear");
    var thursdayConditions = forecastConditionMaker("Thu", "56", "72", "resources/chance_of_rain.gif", "Chance of Rain");
    var fridayConditions = forecastConditionMaker("Fri", "58", "74", "resources/sunny.gif", "Clear");

Bringing the data together, we have a dummy weather forecast for Mountain View, CA::

    var mountainViewForecast = {
        forecast: forecast,
        currentConditions: currentConditions,
        forecastConditions: [tuesdayConditions, wednesdayConditions, thursdayConditions, fridayConditions]
    };

Check the data
-----------------
**Goal: Confirm our data has been correctly populated by using logging**

At this point we've already got quite a bit of code and its worth making sure we haven't made any mistakes.
Using ``forge.logging.log``, we can inspect all the properties of the dummy objects that we've created.

Add this to the end of ``src/js/weather.js``::

    forge.logging.log(mountainViewForecast);

.. _tutorials-weather-tutorial-1-catalyst-debugging:

Remote Debugging on Mobile
-----------------------------
**Goal getting started with Catalyst**

As you've already seen in :ref:`mobile-getting-started` ``forge.logging.log`` prints output to console/terminal.
You can also use our remote debugging tool, Catalyst, which provides some helpful tools for troubleshooting and examining the app at runtime.

For a screencast on Catalyst, and help on how to get started see `Screencast: Trigger.io Catalyst in action <http://trigger.io/cross-platform-application-development-blog/2012/05/04/screencast-trigger-io-catalyst-in-action-2/>`_.

#. Open up a browser and go to http://trigger.io/catalyst/.
#. On this page there will be a generated ``script`` tag which you copy and insert into the head element of your ``index.html`` file.
#. Click on the auto-generated link which takes you to a page that looks similar to Chrome's debugging tools.
#. Open ``src/js/weather.js`` and add the following at the **beginning** of the file::

    window.forge.enableDebug();

This will ensure that Catalyst is connected and ready before the code runs, preventing any logging from being lost.

5. Rebuild and re-run your app. In a few moments, your Catalyst tab in the browser should show the device.
#. Check the console of the Catalyst tool: you should see your ``mountainViewForecast`` object being logged.

.. note:: Catalyst is a great tool, especially for debugging mobile apps: check out the "Elements" view to inspect and modify the DOM, the "API" tab to see your ``forge`` calls flowing back and forth, and the "Network" view to diagnose performance problems.

.. _tutorials-weather-tutorial-1-chrome-debugging:

Debugging on Chrome
---------------------
**Goal: Checking forge.logging.log output in Chrome console**

``forge.logging.log`` output can be seen in the Chrome console.
Since ``weather.js`` is running inside ``index.html`` we need to inspect that page to see the logged output.

* Open up a Chrome browser and go to `<chrome:extensions>`_
* If you have already added your Chrome extension, refresh it (Chrome caches aggressively - refreshing a few times is a good idea)
* If you haven't added your Chrome extension yet, see :ref:`chrome-getting-started-load-extension`
* Right click on the toolbar button that is added by the extension and click **Inspect pop-up**
* This will open up the Chrome developer tools for your popup in a new window
* At the bottom is the console section, which should contain the output from ``forge.logging.log``
* Inspect the logged properties of ``mountainViewForecast`` and make sure everything looks OK

The :ref:`background <extension-concept-background>` context also receives the logging call for debugging convenience.

* Navigate to `<chrome:extensions>`_
* You should see a **Inspect active views** option, with a ``forge.html`` link
* Click ``forge.html`` which will open up the Chrome developer tools for your background page
* The console may not be displayed automatically, but it can be opened by pressing the Esc key or clicking the console button on the bottom left

Reference app
-------------------
`part-1.zip <../../_static/weather/part-1.zip>`_ contains the code you should have in your app's src directory at this point.
Feel free to check your code against it or use it to resume the tutorial from this point.

What next?
-------------------------------------------
Continue on to :ref:`weather-tutorial-2`!

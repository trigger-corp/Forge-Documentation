.. _tutorials-weather-tutorial-1:

Tutorial Part 1
================

In this tutorial, we will step through building a basic weather app using the Forge tools.

This section of the tutorial will guide you through setting up the display,
creating internal data representation, and doing some basic debugging using logging.

When using this tutorial, you should choose a single platform to follow along with: either iOS, Android, mobile website or Chrome extension.
The code we'll be writing will work on any platform, but the configuration steps are different.

The parts that are specific to a platform will be marked with **(Mobile Only)** or **(Chrome Only)**.

All the code for this tutorial is on Github: https://github.com/trigger-corp/weather-app-demo/

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

* Firstly, if you haven't already done so, go through the :ref:`getting started on mobile <mobile-getting-started>` or :ref:`getting started on Chrome <chrome-getting-started>` instructions.
  This will help you set up the basics and teach you how to build and run your code.
* Remove any files in the ``src`` directory except ``config.json``, ``identity.json`` and the ``js`` folder (the other files will not be needed for the rest of this tutorial).
* Sign up for API access at http://www.wunderground.com/weather/api/ - the most basic free developer account is fine.
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
For a Chrome extension a :ref:`toolbar button<modules-button>` will be added near the browsers address bar which will display ``index.html`` when clicked.

Click on your App Config tab in the Toolkit or edit ``config.json`` to add the following configuration to the ``modules`` section.

.. important:: JSON requires all key value pairs to be separated by commas.
    Makes sure to place proceeding or trailing commas as appropriate!

::

    "button": {
        "default_popup": "index.html"
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

First, we will create some dummy data in a simplified version of the format that the Wunderground API will return to us - open ``src/js/weather.js`` and paste the following code:

.. code-block:: js

    var weather = {
        "current_observation": {
            "display_location": {
                "full": "San Francisco, CA"
            },
            "observation_time":"Last Updated on September 20, 3:50 AM PDT",
            "weather": "Mostly Cloudy",
            "temp_f": 54.4,
            "temp_c": 12.4,     
            "relative_humidity":"89%",
            "wind_string":"From the WNW at 4.0 MPH",
            "icon_url":"http://icons-ak.wxug.com/i/c/k/nt_mostlycloudy.gif"
        },
        "forecast": {
            "simpleforecast": {
                "forecastday": [
                    { "date": { "weekday_short": "Thu" },
                      "period": 1,
                      "high": { "fahrenheit": "64", "celsius": "18" },
                      "low": { "fahrenheit": "54", "celsius": "12" },
                      "conditions": "Partly Cloudy",
                      "icon_url":"http://icons-ak.wxug.com/i/c/k/partlycloudy.gif" },
                    { "date": { "weekday_short": "Fri" },
                      "period": 2,
                      "high": { "fahrenheit": "70", "celsius": "21" },
                      "low": { "fahrenheit": "54", "celsius": "12" },
                      "conditions": "Mostly Cloudy",
                      "icon_url":"http://icons-ak.wxug.com/i/c/k/mostlycloudy.gif" },
                    { "date": { "weekday_short": "Sat" },
                      "period": 3,
                      "high": { "fahrenheit": "70", "celsius": "21" },
                      "low": { "fahrenheit": "52", "celsius": "11" },
                      "conditions": "Partly Cloudy",
                      "icon_url":"http://icons-ak.wxug.com/i/c/k/partlycloudy.gif" }
                ]
            }
        }
    };

Check the data
-----------------
**Goal: Confirm our data has been correctly populated by using logging**

If we need to verify that our app is showing the right forecast in the future, it would be useful to log out what data input is. We can use the logging module for this.

Add this to the end of ``js/weather.js``:

.. code-block:: js

    forge.logging.info(JSON.stringify(weather));

.. _tutorials-weather-tutorial-1-catalyst-debugging:

Remote Debugging on Mobile
-----------------------------
**Goal getting started with Catalyst**

As you've already seen in :ref:`getting started on mobile <mobile-getting-started>` ``forge.logging.info`` prints output to console/terminal.
You can also use our remote debugging tool, Catalyst, which provides some helpful tools for troubleshooting and examining the app at runtime.

If you're working with Chrome, you can just use the Chrome Developer tools by right-clicking on the popup: see the next section.

For a screencast on Catalyst, and help on how to get started see `Screencast: Trigger.io Catalyst in action <http://trigger.io/cross-platform-application-development-blog/2012/05/04/screencast-trigger-io-catalyst-in-action-2/>`_.

#. Open up a browser and go to http://trigger.io/catalyst/.
#. On this page there will be a generated ``script`` tag which you copy and insert into the head element of your ``index.html`` file.
#. Click on the auto-generated link which takes you to a page that looks similar to Chrome's debugging tools.
#. Open ``src/js/weather.js`` and add the following at the **beginning** of the file:

.. code-block:: js

    window.forge.enableDebug();

This will ensure that Catalyst is connected and ready before the code runs, preventing any logging from being lost.

5. Rebuild and re-run your app. In a few moments, your Catalyst tab in the browser should show the device.
#. Check the console of the Catalyst tool: you should see your forecast object being logged.

.. note:: Catalyst is a great tool, especially for debugging mobile apps: check out the "Elements" view to inspect and modify the DOM, the "API" tab to see your ``forge`` calls flowing back and forth, and the "Network" view to diagnose performance problems.

.. _tutorials-weather-tutorial-1-chrome-debugging:

Debugging on Chrome
---------------------
**Goal: Checking forge.logging.log output in Chrome console**

``forge.logging.log`` output can be seen in the Chrome console.
Since ``weather.js`` is running inside ``index.html`` we need to inspect that page to see the logged output.

* Open up a Chrome browser and go to `<chrome:extensions>`_
* If you have already added your Chrome extension, refresh it (Chrome caches aggressively - refreshing a few times is a good idea)
* If you haven't added your Chrome extension yet, see :ref:`loading an extension in Chrome <chrome-getting-started-load-extension>`
* Open your app's popup by clicking the toolbar button, right-click and pick **Inspect pop-up**
* This will open up the Chrome developer tools for your popup in a new window
* At the bottom is the console section, which should contain the output from ``forge.logging.log``
* Inspect the logged properties of the forecast object and make sure everything looks OK

The :ref:`background <extension-concept-background>` context also receives the logging call for debugging convenience.

* Navigate to `<chrome:extensions>`_
* You should see a **Inspect active views** option, with a ``forge.html`` link
* Click ``forge.html`` which will open up the Chrome developer tools for your background page
* The console may not be displayed automatically, but it can be opened by pressing the Esc key or clicking the console button on the bottom left

Reference app
-------------
See the ``part-1`` tag in the `Github repository <https://github.com/trigger-corp/weather-app-demo/tree/part-1>`_ for a reference app for this stage of the tutorial.

`part-1.zip <https://github.com/trigger-corp/weather-app-demo/zipball/part-1>`_

What next?
----------
Continue on to :ref:`weather-tutorial-2`!

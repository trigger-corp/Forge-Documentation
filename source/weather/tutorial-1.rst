.. _weather-tutorial-1:

Tutorial Part 1
=================

In this tutorial, we will step through building a basic weather app using the WebMynd Android tools.
This section of the tutorial will guide you through setting up the display,
creating internal data representation, and doing some basic debugging using logging.
The code in this tutorial is platform agnostic, but different configuration steps are be necessary for Chrome and Android.
The parts that are specific to a platform will be marked with **(Chrome Only)** or **(Android Only)**

.. contents::

Goal
----
This part of the tutorial is intended to:

* Show how to add project files
* Set up weather forecast data structures
* Familiarize you with developing and running a basic app using Forge

.. _weather-tutorial-1-preparation:

Preparation
-----------
* Firstly, if you haven't already done so go through the :ref:`Chrome getting started <chrome-getting-started>` or :ref:`android-getting-started` instructions.
  This will help you set up the basics and teach you how to build and run your code.
* Remove any files in the ``src`` directory except ``config.json``, the rest of the files will not be needed for the rest of this tutorial.
* Download `resources.zip <../_static/weather/resources.zip>`_, which contains images and other resources needed for this tutorial; extract the ``resources`` directory to the ``src`` directory.
* **(Chrome Only)** Empty the *background_files* array in ``config.json`` by removing the ``background.js`` reference.
* Create a new javascript file called ``weather.js`` inside the ``src`` directory. This file will contain all of the JavaScript code for the rest of the tutorial.
* Create a file called ``index.html`` inside the ``src`` directory. This will be the html page that displays the forecast information.

.. _weather-tutorial-1-setting-up-the-UI:

Setting up the UI
-----------------
**Goal: Displaying static content**

Open ``index.html`` in your favorite editor and add the following:

.. code-block:: html

    <!DOCTYPE html>
    <html>
     <head>
      <script type="text/javascript" src="weather.js"></script>
     </head>
     <body>
      Weather forecast here.
     </body>
    </html>

Notice the script tag in the head element points to ``weather.js`` file you created earlier.
This file does not need any code at this point.

**(Chrome only)**
For a chrome extension a toolbar button will be added near the browsers address bar and when clicked will display ``index.html``.
Toolbar buttons can have an image to differentiate them from other extension toolbar buttons.
There is an icon ``sun_19.png`` inside the resources directory which is the correct size and provided specifically for this purpose.
Open ``config.json`` and add the following configuration to set up the toolbar button.

.. important:: JSON requires all key value pairs to be separated by commas.
    Makes sure to place proceeding or trailing commas as appropriate wherever you place the ``browser_action`` configuration

::

    "browser_action": {
        "default_popup": "index.html",
        "default_icon": "resources/sun_19.png"
    }


Build and run the code.
Instructions on how to build and load an extension for Chrome can be found :ref:`here<chrome-getting-started-build>`\ .
Instruction on how to build and run an Android app can be found :ref:`here <android-getting-started-build>`\ .

Internal Data Representation
----------------------------
**Goal: Design data representation of a weather forecast**

.. _weather-tutorial-1-forecast-information:

Open ``weather.js`` and paste the following code, which will hold forecast information::

    function ForecastInformation(city, forecastDate) {
        this.city = city;
        this.forecastDate = forecastDate;
        
        return this;
    };

.. _weather-tutorial-1-current-conditions:

Create an object to hold the current conditions. ::

    function CurrentConditions(condition, tempF, humidity, iconSrc, windCondition) {
        this.condition = condition;
        this.tempF = tempF;
        this.humidity = humidity;
        this.img = iconSrc;
        this.windCondition = windCondition;
        
        return this;
    };

.. _weather-tutorial-1-forecast-conditions:

We also need an object to hold forecast conditions for the next few days. ::

    function ForecastConditions(dayOfWeek, low, high, imgSrc, condition){
        this.dayOfWeek = dayOfWeek;
        this.low = low;
        this.high = high;
        this.img = imgSrc;
        this.condition = condition;
        
        return this;
    };

To keep things organized lets have another object that holds all of this information. (Note: ``forecastConditions`` in ``WeatherForecast`` is an array of ``ForecastConditions``) ::

    function WeatherForecast(forecast, currentConditions, forecastConditions) {
        this.forecast = forecast;
        this.currentConditions = currentConditions;
        this.forecastConditions = forecastConditions;
        
        return this;
    };

Populate the Data
-----------------
**Goal: Populate the weather forecast objects with dummy data. Using forge.logging.log**

Now that we have some objects to represent a weather forecast, let's populate them with some dummy data.
At this point make sure that the ``resources`` directory is inside the the ``src`` directory.
It contains icons for displaying weather conditions.
If it is missing or you have accidentally removed it, download `resources.zip <../_static/weather/resources.zip>`_; extract the ``resources`` directory to the ``src`` directory.

**Note: The imgSrc arguments to** :ref:`CurrentConditions<weather-tutorial-1-current-conditions>`
**and** :ref:`ForecastConditions<weather-tutorial-1-forecast-conditions>` **are relative URLs.** ::

    var forecast = new ForecastInformation("Mountain View, CA", "2011-08-09");
    var currentConditions = new CurrentConditions("Clear", "73", "Humidity: 57%", "resources/sunny.gif", "Wind: N at 9 mph");
    var tuesdayConditions = new ForecastConditions("Tue", "58","72", "resources/mostly_sunny.gif","Clear");
    var wednesdayConditions = new ForecastConditions("Wed", "58", "72", "resources/sunny.gif", "Clear");
    var thursdayConditions = new ForecastConditions("Thu", "56", "72", "resources/chance_of_rain.gif", "Chance of Rain");
    var fridayConditions = new ForecastConditions("Fri", "58", "74", "resources/sunny.gif", "Clear");
    
    var mountainViewForecast = new WeatherForecast(forecast, currentConditions,
        [tuesdayConditions, wednesdayConditions, thursdayConditions, fridayConditions]);

At this point we've already got quite a bit of code and its worth making sure we haven't made any mistakes.
Using ``forge.logging.log`` we can inspect all the properties of the dummy objects that we've created. ::

    forge.logging.log(mountainViewForecast);

.. _weather-tutorial-1-chrome-debugging:

Debugging on Chrome
---------------------
**Goal: Checking forge.logging.log output in Chrome console**

``forge.logging.log`` output can be seen in the Chrome console.
Since ``weather.js`` is running inside ``index.html`` we need to inspect that page to see the logged output.

* Open up a Chrome browser and go to `<chrome:extensions>`_.
* You should reload the extension to pick up any changes.
* Right click on the toolbar button that is added by the extension and click **Inspect pop-up**
* This will open up Chrome tools in a new window
* At the bottom is the console section, which should contain the output from ``forge.logging.log``
* Inspect the logged properties of mountainViewForecast and make sure everything looks ok

The :ref:`background <extension-concept-background>` context also receives the logging call for debugging convenience.

* Navigate to `<chrome:extensions>`_
* You should see a *Inspect active views* with ``webmynd.html`` link
* Click ``webmynd.html`` which will open up Chrome tools
* The console may not be displayed automatically, but it can be opened by pressing the Esc key or clicking the console button on the bottom left.
* The background tracks all logging

.. _weather-tutorial-1-catalyst-debugging:

Remote Debugging on Android
-----------------------------
**Goal getting started with Catalyst**

As you've already seen in :ref:`Android Getting Started<android-getting-started>` ``forge.logging.log`` prints output to console/terminal.
You can also use remote debugging which provides some helpful tools for troubleshooting and examining the app at runtime.

#. Open up a browser and go to `<http://catalyst.webmynd.com/>`_.
#. On this page there will be a generated ``script`` tag which you copy and insert into the head element of your ``index.html`` file.
#. Click on the auto-generated link which takes you to a page that looks similar to Chrome's debugging tools.
#. Try :ref:`running <android-getting-started-build>` the code.
   In a few moments you should see the device get picked up in the **Catalyst** section.
#. Open ``weather.js`` and add the following at the **beginning** of the file::

    window.forge.debug = true;

This will ensure that Catalyst is connected and ready before the code runs, preventing any logging from being lost.

.. note:: Catalyst is a great tool, especially for debugging mobile apps: check out the "Elements" view to inspect and modify the DOM, and the "Network" view to diagnose performance problems.

Reference extension
-------------------
`part-1.zip <../_static/weather/part-1.zip>`_ contains the code you should have at this point. Feel free to check your code against it, or use it to resume the tutorial from this point.

It's not working!
-----------------
Things to check:

* The best debugging tool is to add logging using forge.logging.log() throughout the code to track progress
* Make sure that the properties of the dummy objects were populated correctly
* If you used any custom code go back to basics and make modifications only after the tutorial code is running correctly
* Make sure you include the script tag inside ``index.html`` to the correct JavaScript code
* If the documentation is at all unclear or if you're still having issues contact support@webmynd.com with "Weather Tutorial" as the subject

.. **Chrome only**

**Android Only**

* Sometimes the emulator can be buggy and the script hangs on the ``Available device`` section. Simply rerunning the script usually fixes this.
* This :ref:`page<android-weather-troubleshooting>` shows how to troubleshoot some previously encountered errors

Continue on to :ref:`weather-tutorial-2`
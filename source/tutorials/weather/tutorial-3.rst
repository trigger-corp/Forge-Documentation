.. _weather-tutorial-3:

Tutorial Part 3
================
This part of the tutorial will demonstrate how to use the Forge :ref:`request <module-request>` module to retrieve data from the Wunderground API. We will then parse the data to pull the necessary information to generate our internal representation.
We will then parse the data to pull the necessary information to generate our internal representation.

.. contents::
   :backlinks: none

Goal
-----
This part of the tutorial is intended to:

* Show how to do cross-domain requests
* Using forge.request.ajax
* Fetch and display live data

Remove Test Dummy Code
----------------------
**Goal: Remove irrelevant code**

In this part of the tutorial we are going to be fetching live data, so we can remove the dummy data.
Open ``weather.js`` and ...

* Remove the ``var weather = { ... }`` declaration
* Remove the ``forge.logging.log(weather)`` call
* Remove ``populateWeatherConditions`` invocation from the document ready listener
  (Note you do not need to remove the entire jQuery document ready listener as it will be used again in the following sections)

Understanding the Data
----------------------
**Goal: Gain an understanding of what data is available and how it's structured**

If you have not done so already sign up for API access at http://www.wunderground.com/weather/api/ and make a note of your API key.

To request a forecast which includes current conditions from the Weather Underground API you will specify an URL using the following format:

http://api.wunderground.com/api/API_KEY/conditions/forecast/q/STATE/CITY_NAME.json

Replace ``API_KEY`` by your Weather Underground API key, ``STATE`` by the two-letter abbreviation of the city's state and ``CITY_NAME`` by a city name with any spaces replaced by an underscore (``_``).

For example to look up weather in New York City, you could use:

http://api.wunderground.com/api/API_KEY/conditions/forecast/q/NY/New_York.json

The data returned will be JSON formatted with an identical structure as our sample data from the first tutorial though with much more detail.

Our ``forecast_information_tmpl`` template is populated from the ``current_observation.display_location`` and ``current_observation.observation_time`` sections:

.. code-block:: js

    ...
    "current_observation": {
        ...
        "display_location": {
            "full":"New York, NY",
            "latitude":"40.75013351",
            "longitude":"-73.99700928",
            "elevation":"17.00000000"
        },
        "station_id":"KNYNEWYO62",
        "observation_time":"Last Updated on September 21, 4:30 AM EDT",
        ...

The ``current_conditions_tmpl`` template is populated from variables in the ``current_observation`` section:

.. code-block:: js

    ...
    "current_observation": {
        ...
        "weather":"Mostly Cloudy",
        "temp_f":63.7,
        "temp_c":17.6,
        "relative_humidity":"74%",
        "wind_string":"Calm",
        "icon_url":"http://icons-ak.wxug.com/i/c/k/nt_mostlycloudy.gif",
        ...        

Finally, the ``forecast_conditions_tmpl`` template is populated from variables in the ``current_observation.forecast.simple_forecast`` section:

.. code-block:: js

    ...
    "current_observation": {
        ...
    },
    "forecast":{
        "txt_forecast": {
        ...
        },
        "simpleforecast": {
            "forecastday": [
                {"date":{
                    "weekday_short":"Fri",
                },
                 "period":1,
                 "high": {
                     "fahrenheit":"72",
                     "celsius":"22"
                 },
                 "low": {
                     "fahrenheit":"64",
                     "celsius":"18"
                 },
                 ...

.. _tutorials-weather-tutorial-3-permissions:

Adding Permissions
-------------------
Since we are retrieving data from a 3rd party, we need to enable the :ref:`request<modules-request>` module and list the URLs we want to access at run-time.

Either look at the App Config section in the Toolkit, or edit ``config.json`` to add this request module configuration to the ``modules`` object:

.. code-block:: js

    "requests": {
        "permissions": ["http://api.wunderground.com/api/*"]
    }

The items in the ``permissions`` array are match patterns: see http://code.google.com/chrome/extensions/match_patterns.html.

The next time you build, re-creating your app will take longer than usual: changing the configuration of your app means we need to do some work server-side.

Fetching Data
-------------
**Goal: Using forge.request.ajax**

Now that you have a feel for what the returned data looks like, let's add a function to ``weather.js`` that will retrieve this data:

.. code-block:: js

    function getWeatherInfo(location) {
        var api_key = "YOUR_API_KEY";
        forge.logging.info("[getWeatherInfo] getting weather for for " + location);
        forge.request.ajax({
            url: "http://api.wunderground.com/api/" + api_key +
                    "/conditions/forecast/q/" + location + ".json",
            dataType: "json",
            success: function (data) {
                forge.logging.info("[getWeatherInfo] success");
            },
            error: function (error) {
                forge.logging.error("[getWeatherInfo] " + JSON.stringify(error));
            }
        });
    };

``forge.request.ajax`` is similar to the behaviour of jQuery's ``$.ajax``, where we specify the url, dataType to be returned, success and error callbacks.

The returned data is a Document object which can be easily parsed with jQuery.

Remember to specify your weather underground API key or the API request will fail!

.. code-block:: js

    var api_key = "YOUR_API_KEY";

At this point the function doesn't actually do anything with the data but you can test to see if the ajax call succeeded.
For example to look up the forecast in San Francisco add the following code to the document ready listener:

.. code-block:: js

    $(function() {
        getWeatherInfo("CA/San_Francisco");
    });

You can verify that this call is working by checking the console output. Expect to see log output like::

    [FORGE] '[getWeatherInfo] getting weather for for CA/San_Francisco'
    [FORGE] '[getWeatherInfo] success'

- **(Mobile Only)** Check either the command prompt/terminal or console of :ref:`Catalyst <tutorials-weather-tutorial-1-catalyst-debugging>`
- **(Chrome Only)** Check the console of the :ref:`pop-up<tutorials-weather-tutorial-1-chrome-debugging>`


Fetching and Populating Data for a US City
------------------------------------------

Alter the ``getWeatherInfo`` function to take an extra callback parameter that will be called if the retrieval was successful. The code should now look like:

.. code-block:: js

    function getWeatherInfo(location, callback) {
        var api_key = "YOUR_API_KEY";
        forge.logging.info("[getWeatherInfo] getting weather for for " + location);
        forge.request.ajax({
            url: "http://api.wunderground.com/api/" + api_key +
                    "/conditions/forecast/q/" + location + ".json",
            dataType: "json",
            success: function (data) {
                forge.logging.info("[getWeatherInfo] success");
                callback(data);
            },
            error: function (error) {
                forge.logging.error("[getWeatherInfo] " + JSON.stringify(error));
            }
        });
    };

Since we already have a function to populate the GUI we just pass that in as the callback to ``getWeatherInfo``\ .The new call would look like:

.. code-block:: js

    $(function(){
        getWeatherInfo("CA/San_Francisco", populateWeatherConditions);
    });

Rebuild and run the code to see live forecast data displayed.

Reference app
-------------
See the ``part-3`` tag in the `Github repository <https://github.com/trigger-corp/weather-app-demo/tree/part-3>`_ for a reference app for this stage of the tutorial.

`part-3.zip <https://github.com/trigger-corp/weather-app-demo/zipball/part-3>`_

What next?
----------
Continue on to the last part: :ref:`weather-tutorial-4`!

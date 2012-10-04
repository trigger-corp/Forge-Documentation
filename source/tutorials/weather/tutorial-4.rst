.. _weather-tutorial-4:

Tutorial Part 4
=================
In this part of the tutorial we’ll add some UI components that allow the user to select a city and use persistent storage to retrieve the information when the application restarts.

Goal
----
This part of the tutorial is intended to:

* Show how to use persistent storage
* Set up city selection UI
* Add listeners to handle city selection changes

Modyfying the UI
----------------
**Goal: Add city selection UI**

We need to add a drop down which will allow the user to select and get forecast information for a particular city.
Open ``index.html`` and append the following to the body element:

.. code-block:: html

    <div id="options">
        <div id="options_header">Select City</div>
        <select id="city_menu"></select>
    </div>

Populating City Selection
-----------------------------
**Goal: Running code which modifies page content**

* Open ``weather.js`` and remove ``getWeatherInfo("CA/San_Francisco", populateWeatherConditions);`` from the document ready listener.
* In the document ready listener, we will populate a drop-down with some example cities:

.. code-block:: js

    $(function(){
        var cities = [ 
            { name: "London", code: "UK/London" },
            { name: "San Francisco", code: "CA/San_Francisco" },
            { name: "Cape Town", code: "ZA/Cape_Town" },
            { name: "Barcelona", code: "ES/Barcelona" },
            { name: "Boston", code: "NY/Boston" },
            { name: "New York", code: "NY/New_York" },
            { name: "Washington DC", code: "DC/Washington" },
            { name: "Tampa", code: "FL/Tampa" },
            { name: "Houston", code: "AL/Houston" },
            { name: "Montreal", code: "CYUL" },
            { name: "Los Angeles", code: "CA/Los_Angeles" },
            { name: "Miami", code: "FL/Miami" },
            { name: "West Palm Beach", code: "FL/West_Palm_Beach" } 
        ];
        cities.forEach(function(city) { 
            $("#city_menu").append("<option value='" + city.code + "'>" + city.name + "</option>");
        });
    });

Clearing Displayed Data
------------------------------
**Goal: Displaying new data when city selection changes**

When the user selects a new city the first thing we want to do is get rid of the old forecast content.
The ``emptyContent`` function is simply clears the old weather information from the html page.

.. note:: If you decided to have a different layout this function will need to be specific to your custom display.

.. code-block:: js

    function emptyContent() {
        forge.logging.log("[emptyContent] removing old data");
        $("#forecast_information").empty();
        $("#current_conditions").empty();
        $("#forecast_conditions table tr").empty();

        forge.logging.log("[emptyContent] finished emptying content");
    };

This function should be called every time new data is about to be displayed, which is handled by the ``populateWeatherConditions``.
Add the call to ``emptyContent`` at the top of the ``populateWeatherConditions`` function, which should then look like:

.. code-block:: js

    function populateWeatherConditions (weather) {
        var tmpl, output;

        emptyContent(); 

        forge.logging.log("[populateWeatherConditions] beginning populating weather conditions");

        tmpl = $("#forecast_information_tmpl").html();
        output = Mustache.to_html(tmpl, weather.current_observation);
        $("#forecast_information").append(output);
        forge.logging.log("[populateWeatherConditions] finished populating forecast information");

        tmpl = $("#current_conditions_tmpl").html();
        output = Mustache.to_html(tmpl, weather.current_observation);
        $("#current_conditions").append(output);
        forge.logging.log("[populateWeatherConditions] finished populating current conditions");

        tmpl = $("#forecast_conditions_tmpl").html();
        output = Mustache.to_html(tmpl, weather.forecast.simpleforecast);
        $("#forecast_conditions table tr").append(output);
        forge.logging.log("[populateWeatherConditions] finished populating forecast conditions");

        forge.logging.log("[populateWeatherConditions] finished populating weather conditions");
    };

Remembering the previous location
--------------------------------------
**Goal: show different weather reports based on the selected city; and remember the previous selected city**

The following code should be placed inside of the document ready listener.

When a city is selected from the drop-down list, we want to remember it to use it as the default city when the app is restarted.

To do that, we listen for changes to the ``city_menu`` element:

.. code-block:: js

    $("#city_menu").change(function() {
        var city = $("#city_menu option:selected").val();
        forge.prefs.set("city", city);
        getWeatherInfo(city, populateWeatherConditions);
    });

See :ref:`forge.prefs.set<api-prefs-set>`.

Using remembered locations
-----------------------------------------
**Goal: default to the user's previously selected city when they re-open the app**

When the application first runs we want to check if a city has already been saved from a previous run.

- the first time the app is run, this preference will be ``null``, meaning its value has not been set
- if a city has been saved previously, it is selected in the drop-down list

.. code-block:: js

    forge.prefs.get("city", function(resource) {
        if (resource) { // user has previously selected a city
            var city = resource;
        } else { // no previous selection
            var city = "CA/San_Francisco";
        }
        $("#city_menu").val(city);
        $("#city_menu").change();
    }, function (error) {
        forge.logging.error("failed when retrieving city preferences");
        $("#city_menu").val("CA/San_Francisco"); // default;
    });

See :ref:`forge.prefs.get<api-prefs-get>`.

The weather app should now be complete.

* Build and run the code
* Bask in all your glory, you have just written an app using Forge!

Reference app
-------------
See the ``part-4`` tag in the `Github repository <https://github.com/trigger-corp/weather-app-demo/tree/part-4>`_ for a reference app for this stage of the tutorial.

`part-4.zip <https://github.com/trigger-corp/weather-app-demo/zipball/part-4>`_

What's next?
------------
It's easy to run the Weather App on a :ref:`different platform<tutorials-weather-conversion>`.

Here are some :ref:`suggestions<tutorials-weather-extensions>` on how to extend the weather app.

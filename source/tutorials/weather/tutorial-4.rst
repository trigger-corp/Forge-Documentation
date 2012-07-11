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

* Open ``weather.js`` and remove ``getWeatherInfo('Boston', populateWeatherConditions);`` from the document ready listener.
* In the document ready listener, we will populate a drop-down with some example cities::

    $(function(){
        // places I've been
        var cities = ['Boston', 'New York', 'Washington DC', 'Tampa', 'Houston', 'Montreal',
            'Los Angeles', 'Miami', 'West Palm Beach']; //and a few others
        cities.forEach(function(city){
            $('#city_menu').append('<option>'+city+'</option>');
        });
    });

Clearing Displayed Data
------------------------------
**Goal: Displaying new data when city selection changes**

When the user selects a new city the first thing we want to do is get rid of the old forecast content.
The ``emptyContent`` function is simply clears the old weather information from the html page.

.. note:: If you decided to have a different layout this function will need to be specific to your custom display.

::

    function emptyContent(){
        forge.logging.log('removing old data');
        $('#forecast_information').empty();
        $('#current_conditions').empty();
        $('#forecast_conditions table tr').empty();
        
        forge.logging.log('finished emptying content');
    };

This function should be called every time new data is about to be displayed, which is handled by the ``populateWeatherConditions``.
Add the call to ``emptyContent`` at the top of the ``populateWeatherConditions`` function, which should then look like::

    function populateWeatherConditions(weatherCondition) {
        var tmpl, output;
        
        emptyContent();
        
        forge.logging.log('beginning populating weather conditions');
        
        tmpl = $('#forecast_information_tmpl').html();
        output = Mustache.to_html(tmpl, weatherCondition.forecast);
        $('#forecast_information').append(output);
        forge.logging.log('finished populating forecast information');
        
        tmpl = $('#current_conditions_tmpl').html();
        output = Mustache.to_html(tmpl, weatherCondition.currentConditions);
        $('#current_conditions').append(output);
        forge.logging.log('finished populating current conditions');
        
        tmpl = $('#forecast_conditions_tmpl').html();
        output = Mustache.to_html(tmpl, {conditions: weatherCondition.forecastConditions});
        $('#forecast_conditions table tr').append(output);
        forge.logging.log('finished populating forecast conditions');
        
        forge.logging.log('finished populating weather conditions');
    };

Remembering the previous location
--------------------------------------
**Goal: show different weather reports based on the selected city; and remember the previous selected city**

The following code should be placed inside of the document ready listener.

When a city is selected from the drop-down list, we want to remember it to use it as the default city when the app is restarted.

To do that, we listen for changes to the ``city_menu`` element::

    $('#city_menu').change(function() {
        var city = $("#city_menu option:selected").html();
        forge.prefs.set('city', city);
        getWeatherInfo(city, populateWeatherConditions);
    });

See :ref:`forge.prefs.set<api-prefs-set>`.

Using remembered locations
-----------------------------------------
**Goal: default to the user's previously selected city when they re-open the app**

When the application first runs we want to check if a city has already been saved from a previous run.

- the first time the app is run, this preference will be ``null``, meaning its value has not been set
- if a city has been saved previously, it is selected in the drop-down list

::

    forge.prefs.get('city',
        function(resource) {
            if (resource) {
                // user has previously selected a city
                var city = resource;
            } else {
                // no previous selection
                var city = 'Boston';
            }

            $('#city_menu').val(city);
            $('#city_menu').change();
        },
        function (error) {
            forge.logging.error('failed when retrieving city preferences');
            $('#city_menu').val('Boston'); //default;
        }
    );

See :ref:`forge.prefs.get<api-prefs-get>`.

The weather app should now be complete.

* Build and run the code
* Bask in all your glory, you have just written an app using Forge!

Reference app
-------------------
`part-4.zip <../../_static/weather/part-4.zip>`_ contains the code you should have in your app's src directory at this point.
Feel free to check your code against it or use it to resume the tutorial from this point

What's next?
------------
It's easy to run the Weather App on a :ref:`different platform<tutorials-weather-conversion>`.

Here are some :ref:`suggestions<tutorials-weather-extensions>` on how to extend the weather app.

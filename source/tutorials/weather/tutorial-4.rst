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
* Since we will be modifying the page to add cities we need to make sure the page is fully loaded::	

    $(function(){
        //city population code
    });

* Inside of the document ready wrapper create an array and populated with some cities, for example::

    // places I've been
    var cities = ['Boston', 'New York', 'Washington DC', 'Tampa', 'Houston', 'Montreal',
        'Los Angeles', 'Miami', 'West Palm Beach']; //and a few others

* Add the following code which will put each city from the array in the drop down::

    cities.forEach(function(city){
        $('#city_menu').append('<option>'+city+'</option>');
    });

Clearing Displayed Data
------------------------------
**Goal: Displaying new data when city selection changes**

When the user selects a new city the first thing we want to do is get rid of the old content.
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
When a new city is selected we want to store it in local storage, so if the application is restarted the last selected city will be the default selection.

The following code sets up a handler which listens for city change.
When a new city is selected it is saved to preferences, the old content is cleared from the page, and the forecast for the new city is retrieved and displayed.

``forge.prefs.set`` call takes four parameters, the name of the preference to store, the value, success callback and error callback.
The last two parameters can be omitted in this context::

    $('#city_menu').change(function() {
        var city = $("#city_menu option:selected").html();
        forge.prefs.set('city', city);
        getWeatherInfo(city, populateWeatherConditions);
    });

When the application first runs we want to check if a city has already been saved from a previous run.
The first time the app is run, this preference will be ``null``.

If a city has been saved to preferences, it is set as the selection and a change event is fired.
**Note:** Even if the selection changes the change event is not fired until focus is lost, so we fire this event programatically.

``forge.prefs.get`` takes 3 parameters, the name of the preference, a success callback which will be invoked with the value of the requested preference, and a callback if an error occurred retrieving the resource. The following code should be placed inside of the document ready listener.::

    forge.prefs.get('city', function(resource) {
            if(resource) {
                if ($('#city_menu').val() == resource) {
                    $('#city_menu').change();
                } else {
                    //change event is not fired until focus is lost
                    $('#city_menu').val(resource).change();
                }
            }
            else { //default
                getWeatherInfo('Boston', populateWeatherConditions);
            }
        },
        function() {
            forge.logging.log('ERROR! failed when retrieving city preferences');
            $('#city_menu').val('Boston'); //default;
        }
    );

The weather app should now be complete.

* Build and run the code
* Bask in all your glory, you have just written an app using Forge!

Reference extension
-------------------
`part-4.zip <../../_static/weather/part-4.zip>`_ contains the code you should have in your app's src directory at this point.
Feel free to check your code against it or use it to resume the tutorial from this point
(remember to replace the 'author' and 'uuid' values in config.json with your own).

It's not working!
-----------------
Things to check:

* The best debugging tool is to add logging using forge.logging.log() throughout the code to track progress
* Any code that modified the page should be inside the page ready listener.
  This includes city selection population, checking preferences on startup, and city change handling code.

**Mobile Only**

* Use :ref:`Catalyst<tutorials-weather-tutorial-1-catalyst-debugging>` to inspect logging output and html of ``index.html``
* This :ref:`page<mobile-troubleshooting>` shows how to troubleshoot some previously encountered errors

**Chrome only**

* Use Chrome's development tools to set breakpoint, step thorough the code, and evaluate expressions as necessary

What's next?
------------
It's easy to run the Weather App on a :ref:`different platform<tutorials-weather-conversion>`
Here are some :ref:`suggestions<tutorials-weather-extensions>` on how to extend the weather app

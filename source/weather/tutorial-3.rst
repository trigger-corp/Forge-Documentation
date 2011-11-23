.. _weather-tutorial-3:

Tutorial Part 3
================
This part of the tutorial will demonstrate how to use the WebMynd Ajax functionality to retrieve data from the Google weather API.
We will then parse the data to pull the necessary information to generate our internal representation.

.. contents::

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

* Remove ``mountainViewForecast``, ``forecast``, ``currentConditions``, ``tuesdayConditions``, ``wednesdayConditions``, ``thursdayConditions``, ``fridayConditions`` vars
* Remove the ``forge.logging.log(mountainViewForecast)`` call
* Remove ``populateWeatherConditions`` call, just the call not the function.
  You do not need to remove the entire jQuery document ready listener as it will be used again in the following sections

Understanding the Data
----------------------
**Goal: Gain and understanding of what data is available and how it's structured**

In order to see what the returned data will look like, you can put the following into the browser ``http://www.google.com/ig/api?weather=[cityOrZip]``\ .
Replace ``[cityOrZip]`` by a zip code or a city name with any spaces replaced by ``+``.
For example to look up weather in New York City, you could use ``http://www.google.com/ig/api?weather=New+York``

The data returned should look something like the following:

.. code-block:: xml

    <xml_api_reply version="1">
        <weather module_id="0" tab_id="0" mobile_row="0" mobile_zipped="1" row="0" section="0">
            <forecast_information>
                <city data="New York, NY"/>
                <postal_code data="New York"/>
                <latitude_e6 data=""/>
                <longitude_e6 data=""/>
                <forecast_date data="2011-08-22"/>
                <current_date_time data="2011-08-22 16:51:00 +0000"/>
                <unit_system data="US"/>
            </forecast_information>
            <current_conditions>
                <condition data="Mostly Cloudy"/>
                <temp_f data="75"/>
                <temp_c data="24"/>
                <humidity data="Humidity: 46%"/>
                <icon data="/ig/images/weather/mostly_cloudy.gif"/>
                <wind_condition data="Wind: NW at 13 mph"/>
            </current_conditions>
            <forecast_conditions>
                <day_of_week data="Mon"/>
                <low data="61"/>
                <high data="81"/>
                <icon data="/ig/images/weather/mostly_sunny.gif"/>
                <condition data="Mostly Sunny"/>
            </forecast_conditions>
            <forecast_conditions>
                <day_of_week data="Tue"/>
                <low data="63"/>
                <high data="77"/>
                <icon data="/ig/images/weather/sunny.gif"/>
                <condition data="Clear"/>
            </forecast_conditions>
            <forecast_conditions>
                <day_of_week data="Wed"/>
                <low data="67"/>
                <high data="79"/>
                <icon data="/ig/images/weather/sunny.gif"/>
                <condition data="Clear"/>
            </forecast_conditions>
            <forecast_conditions>
                <day_of_week data="Thu"/>
                <low data="68"/>
                <high data="83"/>
                <icon data="/ig/images/weather/chance_of_storm.gif"/>
                <condition data="Chance of Storm"/>
            </forecast_conditions>
        </weather>
    </xml_api_reply>

.. _weather-tutorial-3-permissions:

Adding Permissions
-------------------
Since we are getting data from Google, we need to edit the permissions configuration to allow cross-domain requests.
Open up ``config.json`` and make sure that ``http://www.google.com/*`` is included in the ``permissions`` array::

    "permissions": ["tabs", "http://www.google.com/*"],

Fetching Data
-------------
**Goal: Using forge.ajax**

Now that you have a feel for what the returned data looks like, let's add a function to ``weather.js`` that will retrieve this data::

    function getWeatherInfo(location) {
        forge.logging.log('[getWeatherInfo] getting weather for for '+location);
        forge.ajax({
            url:"http://www.google.com/ig/api?weather="+encodeURIComponent(location),
            dataType: 'xml',
            success: function(data, textStatus, jqXHR){
                forge.logging.log('[getWeatherInfo] success');
            },
            error: function(jqXHR, textStatus, errorThrown){
                forge.logging.log('ERROR! [getWeatherInfo] '+textStatus);
            }
        })
    };

``encodeURIComponent`` is a built-in Javascript function to prepare strings to be used in URLs.

``forge.request.ajax`` mirrors the behaviour of jQuery's ``$.ajax``, where we specify the url, dataType to be returned, success and error callbacks.

The returned data is a Document object which can be easily parsed with jQuery.

At this point the function doesn't actually do anything with the data but you can test to see if the ajax call succeeded.
For example to look up the forecast in Boston add the following code to the :ref:`document ready listener<weather-tutorial-1-ready-listener>`::

    $(function(){
        getWeatherInfo('Boston');
    });

You can verify that this call is working by checking the console output.
**(Chrome Only)** Check the console of the :ref:`pop-up<weather-tutorial-1-chrome-debugging>`:
**(Android Only)** Check either the command prompt/terminal or console of :ref:`Catalyst <weather-tutorial-1-catalyst-debugging>`

Parsing the Data
----------------
**Goal: Extract data to populate internal weather forecast representation**

Now we are going to add some more functions to ``weather.js`` which will extract information from the data we retrieve.

This code will parse relevant information from forecast_information in the returned xml to create a  :ref:`ForecastInformation <weather-tutorial-1-forecast-information>` object::

    function buildForecastInformation(forecastInformation){
        forge.logging.log('[buildForecastInformation] building internal forecast information object');
        
        var city = $('city', forecastInformation).attr('data');
        var forecastDate = $('forecast_date', forecastInformation).attr('data');
        
        return new ForecastInformation(city, forecastDate);
    };

The following code is just a helper function to extract the icon name and return the URL of the resource::

    function formatImgSrc(imgURL){
        return 'resources/'+/[a-z_]*.gif/.exec(imgURL)[0];
    };

To parse the ``current_conditions`` information and create :ref:`CurrentConditions <weather-tutorial-1-current-conditions>` object::

    function buildCurrentCondition(currentCondition){
        forge.logging.log('building internal current conditions object');
        
        var condition = $('condition', currentCondition).attr('data');
        var tempF = $('temp_f', currentCondition).attr('data');
        var humidity = $('humidity', currentCondition).attr('data');
        var imgURL = $('icon', currentCondition).attr('data');
        var img = formatImgSrc(imgURL);
        var windCondition = $('wind_condition', currentCondition).attr('data');
        
        return new CurrentConditions(condition, tempF, humidity, img, windCondition);
    };


Since there are multiple forecast_conditions we can iterate over them and return an array of :ref:`ForecastConditions <weather-tutorial-1-forecast-conditions>` ::

    function buildForecastConditions(forecastConditions){
        var convertedForecastConditions = [];
        $(forecastConditions).each(function(index, element){
            convertedForecastConditions.push(buildForecastCondition(element));
        });
        return convertedForecastConditions;
    };
    
    function buildForecastCondition(forecastCondition){
        forge.logging.log('[buildForecastCondition] building internal forecast condition');
        
        var dayOfWeek = $('day_of_week', forecastCondition).attr('data');
        var low = $('low', forecastCondition).attr('data');
        var high = $('high', forecastCondition).attr('data');
        var imgURL = $('icon', forecastCondition).attr('data');
        var img = formatImgSrc(imgURL);
        var condition = $('condition', forecastCondition).attr('data');
        
        return new ForecastConditions(dayOfWeek, low, high, img, condition);
    };

Tying it all together ::

    function buildWeather(parsedData){
        forge.logging.log('[buildWeather] converting data to internal representation');
        
        var forecastInformation = buildForecastInformation($('forecast_information', parsedData));
        var currentConditions = buildCurrentCondition($('current_conditions', parsedData))
        var forecastConditions = buildForecastConditions($('forecast_conditions', parsedData));
        return new WeatherForecast(forecastInformation, currentConditions, forecastConditions);
    };

Getting and Parsing Data for a US City
--------------------------------------

Alter the ``getWeatherInfo`` function to take an extra callback parameter that will be called if the retrieval was successful. The code should now look like::

    function getWeatherInfo(location, callback){
        forge.logging.log('[getWeatherInfo] getting weather for for '+location);
        forge.request.ajax({
            url:"http://www.google.com/ig/api?weather="+encodeURIComponent(location),
            dataType: 'xml',
            success: function(data, textStatus, jqXHR){
                forge.logging.log('[getWeatherInfo] success');
                var weatherObj = buildWeather(data);
                callback(weatherObj);
            },
            error: function(jqXHR, textStatus, errorThrown){
                forge.logging.log('ERROR! [getWeatherInfo] '+textStatus);
            }
        })
    };

Since we already have a function to populate the GUI we just pass that in as the callback to ``getWeatherInfo``\ .The new call would look like::

    $(function(){
        getWeatherInfo('Boston', populateWeatherConditions);
    });

Rebuild and run the code to see live forecast data displayed.

Reference extension
-------------------
`part-3.zip <../_static/weather/part-3.zip>`_ contains the code you should have at this point. Feel free to check your code against it, or use it to resume the tutorial from this point.

It's not working!
-----------------
Things to check:

* Make sure all of the dummy code from the previous sections is removed
* The best debugging tool is to add logging using forge.logging.log() throughout the code to track progress
* If the ``forge.request.ajax`` call is failing make sure you've added to appropriate :ref:`permissions<weather-tutorial-3-permissions>` to the configuration
* You can validate that the parsing is working as expected by logging out the generated objects and inspecting their properties

**Chrome only**

* Use chromes development tools to set breakpoint, step thorough the code, and evaluate expressions as necessary

**Android Only**

* Use :ref:`Catalyst<weather-tutorial-1-catalyst-debugging>` to inspect logging output and html of ``index.html``
* This :ref:`page<android-weather-troubleshooting>` shows how to troubleshoot some previously encountered errors

Continue on to :ref:`weather-tutorial-4`
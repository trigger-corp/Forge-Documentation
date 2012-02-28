.. _weather-tutorial-3:

Tutorial Part 3
================
This part of the tutorial will demonstrate how to use the Forge Ajax functionality to retrieve data from the Google weather API.
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

* Remove ``mountainViewForecast``, ``forecast``, ``currentConditions``, ``tuesdayConditions``, ``wednesdayConditions``, ``thursdayConditions``, ``fridayConditions`` vars and the ``forecastConditionMaker`` function
* Remove the ``forge.logging.log(mountainViewForecast)`` call
* Remove ``populateWeatherConditions`` invocation from the document ready listener
  (Note you do not need to remove the entire jQuery document ready listener as it will be used again in the following sections)

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
            ...
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

At this point, rebuilding your app will take longer than usual: changing the configuration of your app means we need to do some work server-side.

Fetching Data
-------------
**Goal: Using forge.request.ajax**

Now that you have a feel for what the returned data looks like, let's add a function to ``weather.js`` that will retrieve this data::

    function getWeatherInfo(location) {
        forge.logging.log('[getWeatherInfo] getting weather for for '+location);
        forge.request.ajax({
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

    $(function() {
        getWeatherInfo('Boston');
    });

You can verify that this call is working by checking the console output.
**(Chrome Only)** Check the console of the :ref:`pop-up<weather-tutorial-1-chrome-debugging>`:
**(Android Only)** Check either the command prompt/terminal or console of :ref:`Catalyst <weather-tutorial-1-catalyst-debugging>`

Parsing the Data
----------------
**Goal: Extract data to populate internal weather forecast representation**

Now we are going to add some more functions to ``weather.js`` which will extract information from the data we retrieve.

First, a utility function to transform XML from the Google API into equivalent JSON::

    var xmlToJson = function(doc, keys) {
        /** Transforms an XML document into JSON
    
        doc is a document
        keys is an array of strings, specifying the names of XML nodes to pull from the document
        */
        var result = {};
    
        for (var counter=0; counter<keys.length; counter+=1) {
            result[keys[counter]] = $(keys[counter], doc).attr('data');
        }
        return result;
    }

Secondly, include this helper function to re-point references to icons at the right location::

    function formatImgSrc(imgURL) {
        return 'resources/'+/[a-z_]*.gif/.exec(imgURL)[0];
    };

Next, we'll use ``xmlToJson`` to pull data out of the XML response and into objects with the same structure as the dummy JSON we had originally::

    function buildForecastInformation(forecastInformation) {
        forge.logging.log('[buildForecastInformation] building internal forecast information object');
    
        return xmlToJson(forecastInformation, ['city', 'forecast_date']);
    };
    
    function buildCurrentCondition(currentCondition) {
        forge.logging.log('building current conditions object');
        
        var currentCondition = xmlToJson(currentCondition, ['condition', 'temp_f', 'humidity', 'icon', 'wind_condition']);
        currentCondition['icon'] = formatImgSrc(currentCondition['icon']);
        
        return currentCondition;
    };
    
    function buildForecastConditions(forecastConditions) {
        var convertedForecastConditions = [];
        $(forecastConditions).each(function(index, element) {
            convertedForecastConditions.push(buildForecastCondition(element));
        });
        return convertedForecastConditions;
    };
    
    function buildForecastCondition(forecastCondition) {
        forge.logging.log('[buildForecastCondition] building forecast condition');
        
        var forecastCondition = xmlToJson(forecastCondition, ['day_of_week', 'low', 'high', 'icon', 'condition']);
        forecastCondition['icon'] = formatImgSrc(forecastCondition['icon']);
        
        return forecastCondition;
    };

We can use these functions to create a full weather forecast objects::

    function buildWeather(parsedData) {
        forge.logging.log('[buildWeather] converting data to internal representation');
        
        var forecastInformation = buildForecastInformation($('forecast_information', parsedData));
        var currentConditions = buildCurrentCondition($('current_conditions', parsedData))
        var forecastConditions = buildForecastConditions($('forecast_conditions', parsedData));
        
        return {
            forecast: forecastInformation,
            currentConditions: currentConditions,
            forecastConditions: forecastConditions
        }
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
`part-3.zip <../_static/weather/part-3.zip>`_ contains the code you should have in your app's src directory at this point.
Feel free to check your code against it or use it to resume the tutorial from this point
(remember to replace the 'author' and 'uuid' values in config.json with your own).

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
.. _weather-tutorial-2:

Tutorial Part 2
================

This part of the tutorial will demonstrate how to use the Forge Ajax functionality to retrieve data from the Google weather API.
We will then parse the data to pull the necessary information to generate our internal representation.

.. contents::
   :backlinks: none

Goal
----
This part of the tutorial is intended to:

* Embed external scripts
* Display dynamic data using jQuery templating

Adding jQuery
--------------
**Goal: Embedding jQuery libraries**

jQuery provides a lot of helpful functionality and in order to display the forecast information we will use Mustache Templates.
If you've looked in the ``resources`` directory you might have noticed the jQuery and Mustache libraries. To use these simply append the following script tags in the head of ``index.html`` before the ``weather.js`` script tag:

.. code-block:: html

    <script type="text/javascript" src="resources/jquery.min.js"></script>
    <script type="text/javascript" src="resources/mustache.js"></script>

It's that simple. You can now access jQuery using "$" or "jQuery" inside ``index.html`` and ``weather.js``

Displaying the Data
-------------------
**Goal: Displaying dynamic data**

Using Mustache, it is quite simple to display the data.

* Open ``index.html``
* Remove "Weather forecast here." from the body tag
* Append to the body tag a Mustache template to represent :ref:`forecast information <weather-tutorial-1-forecast-information>`:

.. code-block:: html

    <div class="template" id="forecast_information_tmpl">
        <span>Forecast for {{city}}</span><br/>
        <span>{{forecast_date}}</span>
    </div>

* Next we need a template to render the :ref:`current conditions <weather-tutorial-1-current-conditions>` object:

.. code-block:: html

    <div class="template" id="current_conditions_tmpl">
        <table>
            <tr>
                <td><img src="{{icon}}"></td>
                <td>
                    <div>{{condition}}</div>
                    <div>{{temp_f}}&deg;F</div>
                    <div>{{humidity}}</div>
                    <div>{{wind_condition}}</div>
                </td>
            </tr>
        </table>
    </div>

* And finally add a template for :ref:`forecast conditions <weather-tutorial-1-forecast-conditions>`. Here, we're using `Mustache's Enumerable syntax <https://github.com/janl/mustache.js>`_ to loop through a few days' conditions:

.. code-block:: html

    <div class="template" id="forecast_conditions_tmpl">
        {{#conditions}}
        <td>
            <h2>{{day_of_week}}</h2>
            <img src="{{icon}}">
            <h6>{{condition}}</h6>
            <h6>Low: {{low}}&deg;F</h6>
            <h6>High: {{high}}&deg;F</h6>
        </td>
        {{/conditions}}
    </div>

* Next we need designated elements where the templated information will be appended. Add the following tags following the templates inside the body element:

.. code-block:: html

    <div id="forecast_information"></div>
    
    <div id="current_conditions"></div>
    
    <div id="forecast_conditions">
        <table>
            <tr>
            </tr>
        </table>
    </div>

* Now open ``weather.js`` and add the following JavaScript code which will template and append the data ::

    function populateWeatherConditions(weatherCondition) {
        var tmpl, output;
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

* Finally add a jQuery.ready listener inside ``weather.js`` which will kick things off when the page finishes loading::

    $(function(){
        populateWeatherConditions(mountainViewForecast);
    });

.. _weather-tutorial-1-ready-listener:

.. important:: Any code that modifies the page should only be run when the page is finished loading. The above achieves this using jQuery's document ready listener ``$(function () { //Code here })``.


**(Chrome Only)** :ref:`Build <chrome-getting-started-build>` the code and :ref:`reload <chrome-getting-started-load-extension>` the extension.
When you click on the toolbar button you should see the weather forecast displayed in a pop-up window.

**(Android Only)** :ref:`Build <android-getting-started-build>` the code and :ref:`run <android-getting-started-run>` the app and you should see the dummy weather forecast displayed automatically.

Adding CSS
-----------
You can make the display a bit more pleasant by adding some custom CSS.
The ``resources`` directory contains a file called ``style.css`` which you can use for this purpose.
Link this file in the head element of ``index.html`` to add some basic styling to the Weather App:

.. code-block:: html

    <link rel="stylesheet" type="text/css" href="resources/style.css">

At this point, your app should display static weather data for Mountain View, CA when it is opened.

Reference extension
-------------------
`part-2.zip <../_static/weather/part-2.zip>`_ contains the code you should have in your app's src directory at this point.
Feel free to check your code against it or use it to resume the tutorial from this point
(remember to replace the 'author' and 'uuid' values in config.json with your own).

It's not working!
-----------------
Things to check:

* The best debugging tool is to add logging using ``forge.logging.log()`` throughout the code to track progress
* Make sure that you have downloaded the :ref:`resources<weather-tutorial-1-preparation>` and that the paths to the specific resources are correct
* Check that the jQuery script tags appear before the ``weather.js`` script tag inside of ``index.html`` head tag
* ``populateWeatherConditions`` invocation should be inside the document ready listener (modifications to the page should not be made until it finishes loading)

**Chrome only**

* Use chromes development tools to set breakpoint, step thorough the code, and evaluate expressions as necessary

**Android Only**

* Use :ref:`Catalyst<weather-tutorial-1-catalyst-debugging>` to inspect logging output and html of ``index.html``
* This :ref:`page<android-weather-troubleshooting>` shows how to troubleshoot some previously encountered errors

Continue on to :ref:`weather-tutorial-3`
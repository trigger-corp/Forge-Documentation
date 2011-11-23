.. _weather-tutorial-2:

Tutorial Part 2
================

This part of the tutorial will demonstrate how to use the WebMynd Ajax functionality to retrieve data from the Google weather API.
We will then parse the data to pull the necessary information to generate our internal representation.

.. contents::

Goal
----
This part of the tutorial is intended to:

* Embed external scripts
* Display dynamic data using jQuery templating

Adding jQuery
--------------
**Goal: Embedding jQuery libraries**

jQuery provides a lot of helpful functionality and in order to display the forecast information we will use jQuery Templating.
If you've looked in the ``resources`` directory you might have noticed the jQuery and jQuery templating libraries. To use these
simply append the following script tags in the head of ``index.html`` before the ``weather.js`` script tag:

.. code-block:: html

    <script type="text/javascript" src="resources/jquery.min.js"></script>
    <script type="text/javascript" src="resources/jquery.tmpl.min.js"></script>

It's that simple. You can now access jQuery using "$" or "jQuery" inside ``index.html`` and ``weather.js``

Displaying the Data
-------------------
**Goal: Displaying dynamic data**

Using jQuery templating, it is quite simple to display the data.

* Open ``index.html``
* Remove "Weather forecast here." from the body tag
* Append to the body tag a jQuery template to represent :ref:`ForecastInformation <weather-tutorial-1-forecast-information>` :

.. code-block:: html

    <script id="forecast_information_tmpl" type="text/x-jquery-tmpl">
        <span>Forecast for ${city}</span><br/>
        <span>${forecastDate}</span>
    </script>

* Next we need a template to render the :ref:`CurrentConditions <weather-tutorial-1-current-conditions>` object :

.. code-block:: html

    <script id="current_conditions_tmpl" type="text/x-jquery-tmpl">
    <table>
        <tr>
            <td><img src=${img}></td>
            <td>
                <div>${condition}</div>
                <div>${tempF}&deg;F</div>
                <div>${humidity}</div>
                <div>${windCondition}</div>
            </td>
        </tr>
    </table>
    </script>

* And finally add a template for :ref:`ForecastConditions<weather-tutorial-1-forecast-conditions>`. **Note: The following template generates a table column**:

.. code-block:: html

    <script id="forecast_conditions_tmpl" type="text/x-jquery-tmpl">
        <td>
            <h2>${dayOfWeek}</h2>
            <img src=${img}>
            <h6>${condition}</h6>
            <h6>Low: ${low}&deg;F</h6>
            <h6>High: ${high}&deg;F</h6>
        </td>
    </script>

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

    function populateWeatherConditions(weatherCondition){
        forge.logging.log('beginning populating weather conditions');
        
        $('#forecast_information_tmpl').tmpl(weatherCondition.forecast).appendTo($('#forecast_information'));
        forge.logging.log('finished populating forecast information');
        
        $('#current_conditions_tmpl').tmpl(weatherCondition.currentConditions).appendTo($('#current_conditions'));
        forge.logging.log('finished populating current conditions');
        
        $('#forecast_conditions_tmpl').tmpl(weatherCondition.forecastConditions).appendTo($('#forecast_conditions table tr'));
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
Link this file in the head element of ``index.html`` to add some basic styling to the Weather App. :

.. code-block:: html

	<link rel="stylesheet" type="text/css" href="resources/style.css">

Reference extension
-------------------
`part-2.zip <../_static/weather/part-2.zip>`_ contains the code you should have at this point. Feel free to check your code against it, or use it to resume the tutorial from this point.

It's not working!
-----------------
Things to check:

* The best debugging tool is to add logging using forge.logging.log() throughout the code to track progress
* Make sure that you have downloaded the :ref:`resources<weather-tutorial-1-preparation>` and that the paths to the specific resources are correct
* Check that the jQuery script tags appear before the ``weather.js`` script tag inside of ``index.html`` head tag
* The jQuery templating variable references should match the variable names inside your weather forecast objects
* ``populateWeatherConditions`` invocation should be inside the document ready listener. Modifications to the page should not be made until it finishes loading.

**Chrome only**

* Use chromes development tools to set breakpoint, step thorough the code, and evaluate expressions as necessary

**Android Only**

* Use :ref:`Catalyst<weather-tutorial-1-catalyst-debugging>` to inspect logging output and html of ``index.html``
* This :ref:`page<android-weather-troubleshooting>` shows how to troubleshoot some previously encountered errors

Continue on to :ref:`weather-tutorial-3`
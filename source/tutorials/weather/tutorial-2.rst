.. _weather-tutorial-2:

Tutorial Part 2
================

This part of the tutorial will demonstrate how to use the Forge ``request`` module to retrieve data from the Wunderground API.
We will then parse the data to pull the necessary information to generate our internal representation.

.. contents::
   :backlinks: none

Goal
----
This part of the tutorial is intended to:

* Embed external scripts
* Display dynamic data using jQuery templating

Adding external libraries
--------------------------------------------------------------------------------
**Goal: Embedding jQuery and Mustache libraries**

jQuery provides a lot of helpful functionality, and in order to display the forecast information we will use Mustache Templates.

Download the jQuery and Mustache from their project pages and save them in the ``js`` directory.

To use these libraries in your app simply append the following script tags in the head of ``index.html`` before the ``js/weather.js`` script tag:

.. code-block:: html

    <script type="text/javascript" src="js/jquery.min.js"></script>
    <script type="text/javascript" src="js/mustache.min.js"></script>

It's that simple. You can now access jQuery using "$" or "jQuery" inside ``index.html`` and ``weather.js``.

Displaying the Data
-------------------
**Goal: Displaying dynamic data**

Using Mustache, it is quite simple to display the data.

.. note:: To prevent attempts to parse Mustache or other templates as HTML, we recommend wrapping them in script tags with custom type attributes

* Open ``index.html``
* Remove "Weather forecast here." from the body tag
* Append to the body tag a Mustache template to represent the forecast information:

.. code-block:: html

    <script type="x-mustache-template" id="forecast_information_tmpl">
        <span>Forecast for {{city}}</span><br/>
        <span>{{forecast_date}}</span>
        <table>
        {{#conditions}}
            <tr>
                <td>
                    <h2>{{title}}</h2>
                    <img src="{{icon_url}}">
                    <h6>{{fcttxt}}</h6>
                </td>
            </tr>
        {{/conditions}}
        </table>
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

* Now open ``weather.js`` and add the following JavaScript code which will template and append the data:

.. code-block:: js

    function populateWeatherConditions (weatherCondition) {
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

* Finally add a jQuery.ready listener inside ``weather.js`` which will kick things off when the page finishes loading:

.. code-block:: js

    $(function () {
        populateWeatherConditions(mountainViewForecast);
    });

.. _weather-tutorial-1-ready-listener:

.. important:: Any code that modifies the page should only be run when the page is finished loading. The above achieves this using jQuery's document ready listener ``$(function () { /* code here */ })``.

**(Mobile Only)** :ref:`Build <mobile-getting-started-build>` the code and :ref:`run <mobile-getting-started-run>` the app and you should see the dummy weather forecast displayed automatically.

**(Chrome Only)** :ref:`Build <chrome-getting-started-build>` the code and :ref:`reload <chrome-getting-started-load-extension>` the extension.
When you click on the toolbar button you should see the weather forecast displayed in a pop-up window.

Adding CSS
-----------
You can make the display a bit more pleasant by adding some custom CSS.
The ``resources`` directory contains a file called ``style.css`` which you can use for this purpose.
Link this file in the head element of ``index.html`` to add some basic styling to the Weather App:

.. code-block:: html

    <link rel="stylesheet" type="text/css" href="resources/style.css">

At this point, your app should display static weather data for Mountain View, CA when it is opened.

.. image:: /_static/images/part-1_weather.png
    :width: 200px

Reference app
-------------------
`part-2.zip <../../_static/weather/part-2.zip>`_ contains the code you should have in your app's src directory at this point.
Feel free to check your code against it or use it to resume the tutorial from this point.

What next?
------------------------------------
Continue on to :ref:`weather-tutorial-3`!

.. _tutorials-weather-extensions:

Possible Extensions
===================

If the tutorial has piqued your interest and you are looking for
some more improvements to the weather app here are a few suggestions

* The current display is not exactly impressive. Why not add some css or change up the layout?
* Custom themes. Have a UI that allows the user to select a theme which is saved to preferences and persists after restarts
* Set the color of the temperature based on a numeric range
* The returned xml provides fahrenheit as well as celsius, get creative
* This is a big one

    * Use geolocation to determine the current lat/lng
    * Using reverse geocoding determine the current city (this is a tough one, unless you pay Google to use their API)
    * Use the information to look up the forecast for the current location

You could take a look at the :ref:`Forge API<api>` documentation to help you implement this functionality or as a source of inspiration.
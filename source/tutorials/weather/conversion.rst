.. _tutorials-weather-conversion:

Weather App Conversion
=======================
One of the key benefits of using Forge is being able to generate for multiple platforms from the same source code.
Converting the Weather App from Chrome to mobile and vice-versa is as simple as making a few tweaks to the configuration file.

Chrome to Mobile
------------------
If you did the Weather App tutorial using a Chrome extension you do not need to make any modifications at all.
Simply go through the :ref:`Mobile getting started<mobile-getting-started>` section which will show you how to set up the development environment.
Once you have the JDK, SDK and AVD configured simply follow the directions on how to :ref:`build<mobile-getting-started-build>` and :ref:`run<mobile-getting-started-build>` the app.


Mobile to Chrome
-----------------
The code used for building the Chrome extension will be identical, but we just need a way to display ``index.html``.

One option is to have it show up as a popup that appears when a user clicks a toolbar button.
To configure this, simply add the following button configuration to the ``modules`` section in ``config.json`` directory::

    "button": {
        "default_popup": "index.html"
    },

- the *default_popup* setting points to the HTML file that should be displayed when the toolbar button is clicked

If you want to know more about the configuration file, see the :ref:`Config File Reference<config>`.

Now just :ref:`build<chrome-getting-started-build>` and :ref:`load<chrome-getting-started-load-extension>` the extension to see the Weather Demo in Chrome.

Extensions and API
-------------------
This has been only a simple demo of what Forge is capable of.
You can try extending the weather app with your own custom functionality. :ref:`Here<tutorials-weather-extensions>` are a few suggestions to get you going.
Also take a look at the :ref:`API documentation<modules>` to see what type of functionality is provided by Forge.

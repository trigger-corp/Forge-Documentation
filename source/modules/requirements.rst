.. _modules-requirements:

``requirements``: App requirements
================================================================================

The ``requirements`` module allows you to set specific device requirements for your apps.

Config
------

.. parsed-literal::
    {
        "requirements": {
            "android": {
                "minimum_version": "6",
                "disable_ics_acceleration": true
            },
            "ios": {
                "minimum_version": "4.3"
            },
            "chrome": {
                "content_security_policy": "script-src 'self' https://ssl.google-analytics.com; object-src 'self'",
                "web_accessible_resources": [
                    "background.jpg"
                ]
            }
        }
    }

Android
~~~~~~~

* ``minimum version``: the minimum Android API level you want to support, it must be between 5 and 15. More details can be found on the Android developers site: http://developer.android.com/guide/appendix/api-levels.html.
* ``disable_ics_acceleration``: Disables hardware acceleration on Android 4.0, this is a workaround to potential rendering issues which can affect some apps on this particular version of Android.

iOS
~~~

The iOS version is the minimum iOS version you want to support, between 4.0 and 5.1.

Chrome
~~~~~~

The Chrome options relate to Chromes "manifest_version": 2 changes, which are documented on the Chrome website http://code.google.com/chrome/extensions/manifestVersion.html. The available settings are:

* ``content_security_policy``: This determines what javascript can be executed in pages that belong to your extension (such as popups). The example given above is how you would allow Google Analytics to work within an extension. More documentation is available on the Chrome site http://code.google.com/chrome/extensions/contentSecurityPolicy.html
* ``web_accessible_resources``: This is an array of any files in your extension which are to be accessed from external sites. The most common use of this is if your extension uses a content script to load images from your extension into a 3rd party site.
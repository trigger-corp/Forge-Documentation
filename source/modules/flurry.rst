.. _modules-flurry:

``flurry``: Analytics with Flurry
==================================

The ``forge.flurry`` APIs allow you to access the native Flurry SDK, which provides usage tracking and analytics via `Flurry <http://www.flurry.com/>`_.

Before you can use this module, you will need to have set up a Flurry application, and know its API key.

Config
------

The ``flurry`` module must be enabled in ``config.json`` with API keys specified for Android and/or iOS.

.. parsed-literal::
    {
        "modules": {
            "flurry": {
                "android_api_key": "VMGKY81MY88PCDR38ARM",
                "ios_api_key": "3RAG3ZW4QXMRVNJH092S"
            }
        }
    }

By just including this configuration in your app config, basic app analytics
information - such as sessions, active users and new users - will be availabe
in your Flurry dashboard.

For more advanced analytics, you can use the API methods described below.

API
---

``flurry.customEvent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Register a named and optionally parameterised event with Flurry. You could use this to track a user's navigation through your app, for example.

.. js:function:: flurry.customEvent(name, [parameters, ]success, error)

    :param string name: a name to identify this event
    :param object parameters: an optional hash of extra information that will be stored with this event
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``flurry.startTimedEvent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Takes the same options as ``flurry.customEvent``, but using
``flurry.endTimedEvent`` you are able to easily measure the time it takes for
your users to move from one action to another in your app.

.. js:function:: flurry.startTimedEvent(name, [parameters, ]success, error)

    :param string name: a name to identify this event
    :param object parameters: an optional hash of extra information that will be stored with this event
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``flurry.endTimedEvent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Mark the end of a particular timed event: the ``name`` parameter should match
the ``name`` parameter passed into ``flurry.startTimedEvent``.

.. js:function:: flurry.endTimedEvent(name, success, error)

    :param string name: a name to identify this event: should match the name passed into ``flurry.startTimedEvent``
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``flurry.setDemographics``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Store some demographic data about the current user, to enable more advanced
filtering and grouping in the Flurry dashboard.

The ``demographics`` object should contain some or all of these keys:

* ``user_id``: (string) a unique ID for the current user
* ``age``: (number) the current user's age
* ``gender``: (string) either "m" or "f"

.. js:function:: flurry.setDemographics(demographics, success, error)

    :param string demographics: a hash optionally including values for ``user_id``, ``age`` and ``gender``
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

``flurry.setLocation``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Set the user's current location: we recommend you use the :ref:`geolocation
<modules-geolocation>` module to grab the coords object which should be passed
in. E.g.::

    forge.geolocation.getCurrentPosition( function (position) {
        forge.flurry.setLocation(position.coords);
    });

.. js:function:: flurry.setLocation(coords, success, error)

    :param object coords: hash representing location - must include ``latitude``, ``longitude`` and ``accuracy``.
    :param function(response) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur


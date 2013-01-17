.. _modules-calendar:

``calendar``: Calendar manipulation
=======================================

The ``forge.calendar`` namespace allows calendar events to be added to the native calendar

Config
------

The ``calendar`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "calendar": true
        }
    }

API
---

``addEvent``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Show a UI that allows the user to add a calendar event, with certain properties pre-filled.

The properties that can be set are:

* ``title``: The title of the event
* ``description``: The event description (appears as notes on iOS)
* ``location``: The location of the event
* ``start``: The time the event starts (A Javascript ``Date`` object)
* ``end``: The time the event ends (A Javascript ``Date`` object)
* ``allday``: A boolean value that determines whether the event is an all day event (the time of day in the start and end will be ignored in all day events)
* ``recurring``: Whether the event is recurring and how often, one of: ``not``, ``daily``, ``weekly``, ``monthly``, or ``yearly``. If not specified the event will not recur.

Example::

   forge.calendar.addEvent({
       title: "Anniversary of adding my first event",
       start: new Date(),
       end: new Date(),
       allday: true,
       recurring: "yearly"
   }, function () {
       alert("Event added!");
   });

.. js:function:: calendar.addEvent(details, success, error)

    :param function(value) success: callback to be invoked when no errors occur, on Android even if the user cancels adding the event this callback will fire.
    :param function(content) error: called with details of any error which may occur

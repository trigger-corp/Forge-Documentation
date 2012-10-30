.. _native_plugins_javascript_events:

.. role:: inline-html(raw)
   :format: html

Triggering Javascript events
============================

There are two distinct types of events in plugins:

* **Javascript events** which can be triggered from native code at any point, used
  for situations that aren't a direct response to an API method call.
* **Native events** which are points in an application's execution that plugins
  can hook into and execute their own code. For example plugins can execute
  native code on application start, without having to use any Javascript.

Quite frequently you'll want to handle a native event and trigger and trigger a corresponding
Javascript event. This section of the plugin docs will discuss the second type of event, those which
are triggered by the device. If you're interested in the second type of event described, see
:ref:`native_plugins_native_events`.

Javascript
----------

An example of listening for a Javascript event is included in the inspector
project::

    forge.internal.addEventListener("alert.resume", function () {
        alert("Welcome back!");
    });

* Events are identified by a unique string, it is conventional to use the
  format ``plugin.eventName`` for this string as shown above.
* The second parameter is a callback to be invoked whenever the event is
  triggered from native code: data can be passed in the first parameter to this
  callback.

Android
-------

To trigger a Javascript event from native Android code, the
:inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeApp.html#event(java.lang.String, org.json.JSONObject)">ForgeApp.event()</a>`
method can be called at any point. For example::

    ForgeApp.event("alert.resume", null);

* The first parameter is the event identification string which is listened for
  in Javascript.
* The second is an optional object to pass back to Javascript.

iOS
---

To trigger Javascript events from native iOS code, use ``[ForgeApp event]`` at
any point. For example:

.. code-block:: objective-c

    [[ForgeApp sharedApp] event:@"alert.resume" withParam:nil];

* The first parameter is the event identification string which is listened for
  in Javascript.
* The second is an optional object to pass back to Javascript.
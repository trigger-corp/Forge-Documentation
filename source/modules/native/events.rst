.. _native_plugins_events:

Events
======

There are two distinct types of events in plugins:

* Javascript events, which can be triggered from native code at any point, used for situations that aren't a direct response to an API method call.
* Native events, which are points in an application's execution that plugins can hook into and execute their own code. For example plugins can execute native code on application start, without having to use any Javascript.

This section of the plugin docs will discuss how to handle both types of events in the various parts of a plugin.

Javascript
----------

An example of listening for a Javascript event is included in the inspector project::

    forge.internal.addEventListener("alert.resume", function () {
        alert("Weclome back!");
    });

* Events are identified by a unique string, it is conventional to use the format ``plugin.eventName`` for this string as shown above.
* The second parameter is a callback to be invoked whenever the event is triggered from native code: data can be passed in the first parameter to this callback.

Android
-------

Javascript events
~~~~~~~~~~~~~~~~~

To trigger a Javascript event from native Android code, the ``ForgeApp.event()`` method can be called at any point. For example::
    
    ForgeApp.event("alert.resume", null);

* The first parameter is the event identification string which is listened for in Javascript.
* The second is an optional object to pass back to Javascript.

Native events
~~~~~~~~~~~~~

To listen for native events in Android an ``EventListener`` class must be added to your plugin's package. For example, ``io.trigger.forge.android.modules.alert.EventListener``. This class should extend the ``ForgeEventListener`` class and implement any of the methods it wants to listen for.

The example EventListener from the inspector project looks like::

    public class EventListener extends ForgeEventListener {
        @Override
        public void onRestart() {
            ForgeApp.event("alert.resume", null);
        }
    }

* ``@Override`` on the method ensures the method exists in ForgeEventListener and is an available event.
* If you want to prevent subsequent event listeners from receiving an event,
  you should return a non-``null`` value. For example, if a key press event is
  handled by a plugin it can return ``true`` and prevent other plugins from
  seeing the event.

iOS
---

Javascript events
~~~~~~~~~~~~~~~~~

To trigger Javascript events from native iOS code, use ``[ForgeApp event]`` at any point. For example::

    [[ForgeApp sharedApp] event:@"alert.resume" withParam:nil];

* The first parameter is the event identification string which is listened for in Javascript.
* The second is an optional object to pass back to Javascript.

Native events
~~~~~~~~~~~~~

To listen for native events in iOS a class called ``<plugin>_EventListener`` must be created. Where ``<plugin>`` is your plugin name. This class should extend ``ForgeEventListener`` and implement any of the methods it wants to listen for.

The example EventListener from the inspector project looks like::

    @interface alert_EventListener : ForgeEventListener

    @end

    @implementation alert_EventListener

    + (void)applicationWillEnterForeground:(UIApplication *)application {
        [[ForgeApp sharedApp] event:@"alert.resume" withParam:nil];
    }

    @end

* If you want to prevent subsequent event listeners from receiving an event,
  you should return a non-``nil`` value. For example, if a key press event is
  handled by a plugin it can return ``YES`` and prevent other plugins from
  seeing the event.

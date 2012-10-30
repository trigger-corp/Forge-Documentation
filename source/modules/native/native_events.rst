.. _native_plugins_native_events:

.. role:: inline-html(raw)
   :format: html

Handling native events
======================

There are two distinct types of events in plugins:

* **Javascript events** which can be triggered from native code at any point, used
  for situations that aren't a direct response to an API method call.
* **Native events** which are points in an application's execution that plugins
  can hook into and execute their own code. For example plugins can execute
  native code on application start, without having to use any Javascript.

Quite frequently you'll want to handle a native event and trigger and trigger a corresponding
Javascript event. This section of the plugin docs will discuss the second type of event, those which
are triggered by the device. If you're interested in the first type of event described, see
:ref:`native_plugins_javascript_events`.

Android
-------

To listen for native events in Android an ``EventListener`` class must be added
to your plugin's package. For example,
``io.trigger.forge.android.modules.alert.EventListener``. This class should
extend the ``ForgeEventListener`` class and implement any of the methods it
wants to listen for. See the :inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeEventListener.html">Javadoc for ForgeEventListener</a>` for the list of methods available for override as well as their meaning.

The example EventListener from the inspector project looks like:

.. code-block:: java

    public class EventListener extends ForgeEventListener {
        @Override
        public void onRestart() {
            ForgeApp.event("alert.resume", null);
        }
    }

* ``@Override`` on the method ensures the method exists in ForgeEventListener
  and is an available event.
* If you want to prevent subsequent event listeners from receiving an event,
  you should return a non-``null`` value. For example, if a key press event is
  handled by a plugin it can return ``true`` and prevent other plugins from
  seeing the event.

iOS
---

To listen for native events in iOS,  a class called ``<plugin>_EventListener``
must be created where ``<plugin>`` is your plugin name. This class should
extend ``ForgeEventListener`` and implement any of the methods it wants to
listen for. See the :inline-html:`<a href="../../_static/native/ios/Classes/ForgeEventListener.html">appledocs for ForgeEventListener</a>` for the list of methods available for override as well as their meaning.

The example EventListener from the inspector project looks like:

.. code-block:: objective-c

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

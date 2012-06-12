.. _faq:

Frequently Asked Questions
==========================

If you have a question that isn't answered here, try asking on `StackOverflow <http://stackoverflow.com/>`_, email support@trigger.io or join us in `#forge on irc.trigger.io <http://irc.trigger.io/>`_.

Android
----------------

**Problem: When running forge build you receive a stack track with the error "Cannot create a file when that file already exists"**

.. image:: /_static/android/weather/images/troubleshooting/dev-build-fail.png

This is caused by a process locking a directory we need to delete. It might be caused by an AVD or a file explorer window, for example.

Close any running AVD. On Windows it may be necessary to open Task Manager and end ``adb.exe`` manually.

**Problem: I created an AVD to use in the emulator but none of my apps work**

There is a bug in the Android 2.3 emulator that will render your apps unusable: if you manage your own Android AVD you **must** use an Android 2.2 level AVD.

Building and running apps
-----------------------------------

**Why do my apps build really quickly sometimes, and take longer other times?**

Whenever possible, we don't re-generate your whole app: we cache templates locally and adapt them with your new code.

If you make certain changes to your ``config.json`` file, we may have to re-generate these templates, which means a build takes longer.


Catalyst
--------

**Problem: Catalyst does not recognize the device**
    .. image:: /_static/android/weather/images/troubleshooting/catalyst-no-device.png

Catalyst generates a unique id for the script tag every time the page is loaded.
Compare the hash(#) tag in the generated link and the script tag that you appended to the head element to make sure they're the same.
:ref:`Run your app <mobile-getting-started-run>` and once the emulator has loaded your code you should see the device picked up by Catalyst.
More information can be found on the `Catalyst home page <http://trigger.io/catalyst/>`_

    .. image:: /_static/android/weather/images/troubleshooting/catalyst-device-found.png

**No logging shows up in the Catalyst console**

Logging calls may execute before the Catalyst console is ready.
To display logging in Catalyst make sure you include ``window.forge.enableDebug();`` at the top of your Javascript.::

	window.forge.enableDebug();

This will prevent logging until the Catalyst console is ready.
For more information check out the **Advanced usage** section of the `Catalyst homepage <http://trigger.io/catalyst/>`_.

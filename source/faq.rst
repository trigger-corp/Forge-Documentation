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

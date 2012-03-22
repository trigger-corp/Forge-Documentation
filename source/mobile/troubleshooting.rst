.. _mobile-troubleshooting:

Troubleshooting
===============

This page seeks to help troubleshoot common issues.
If it does not solve your issue, please contact support@trigger.io with "Weather Tutorial" as the subject.

Android Building
----------------
.. _mobile-troubleshooting-build-fail:

**Problem: When running forge build you receive a stack track with the error "Cannot create a file when that file already exists"**
	.. image:: /_static/android/weather/images/troubleshooting/dev-build-fail.png

This might be caused by an AVD which has a hold of the resources you are trying to replace.
Close any running AVD. On Windows it may be necessary to open Task Manager and end ``adb.exe`` manually.


Catalyst
--------
.. _mobile-troubleshooting-catalyst-device-not-detected:

**Problem: Catalyst does not recognize the device**
    .. image:: /_static/android/weather/images/troubleshooting/catalyst-no-device.png

Catalyst generates a unique id for the script tag every time the page is loaded.
Compare the hash(#) tag in the generated link and the script tag that you appended to the head element to make sure they're the same.
:ref:`Run your app <mobile-getting-started-run>` and once the emulator has loaded your code you should see the device picked up by Catalyst.
More information can be found on the `Catalyst home page <http://trigger.io/catalyst/>`_

    .. image:: /_static/android/weather/images/troubleshooting/catalyst-device-found.png

.. _mobile-troubleshooting-catalyst-no-logging:

**No logging shows up in the Catalyst console**

Logging calls may execute before the Catalyst console is ready.
To display logging in Catalyst make sure you include ``window.forge.debug = true;`` at the top of your Javascript. ::

	window.forge.debug = true;

This will prevent logging until the Catalyst console is ready.
For more information check out the **Advanced usage** section of the `Catalyst homepage <http://trigger.io/catalyst/>`_.

.. _mobile-running:

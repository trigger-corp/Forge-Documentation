.. _release-notes:

Release Notes
===============================================================================

This file contains information about new features and capabilities of Forge versions, along with migration information for how to upgrade from one level to another.

v1.2 (*current version*)
-------------------------------------------------------------------------------

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* Firefox
* iOS

.. _upgrade-1.2:

Upgrade Instructions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All new apps are now created at v1.2 by default. To update an existing app, change your ``platform_version`` setting from ``v1.1`` to ``v1.2``::

    "platform_version": "v1.2"

In v1.2, the ``libs`` directive in the configuration file has become an object, rather than an array, to allow for future extension.

Where you before had::

    "libs": []

You should now include::

    "libs": {}

.. note:: to enable the new Gmail library, ``libs`` should be::

    "libs": { "gmail": {} }

.. note:: ``libs`` has also been made optional, so you can remove it from your configuration file entirely if you wish

For API information, see http://docs.trigger.io/en/v1.2/api/index.html

v1.1 (*unsupported*)
-------------------------------------------------------------------------------
Earliest available Forge platform version.

.. important:: v1.1 of the platform is now unsupported and any attempt to build with this level will fail.

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* Firefox
* iOS

For API information, see http://docs.trigger.io/en/v1.1/api/index.html
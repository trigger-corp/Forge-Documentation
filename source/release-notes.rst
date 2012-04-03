.. _release-notes:

Release Notes
===============================================================================

This file contains information about new features and capabilities of Forge versions, along with migration information for how to upgrade from one level to another.

v1.3 (*current version*)
-------------------------------------------------------------------------------

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* Firefox
* iOS
* Web

Changes from v1.2
~~~~~~~~~~~~~~~~~

The v1.3 platform release changes the format of config.json to put most optional configuration into separate modules, this allows Forge to provide more features without having them all enabled for every app.

By default all of the features from v1.2 will be enabled, but these can be disabled if not required. Disabled modules allow the Forge generation process to remove code from your app, making it smaller. Modules also define the permissions your app will required, so disabled unused modules will reduce the permissions users are prompted for when installing your app.

.. _upgrade-1.3:

Upgrade Instructions
~~~~~~~~~~~~~~~~~~~~

To upgrade from v1.2 to v1.3 your ``config.json`` file needs to be updated, this can be done automatically by running ``forge migrate`` with the command line tools, or choosing to migrate from Trigger Toolkit.

The migration process will automatically update your ``config.json`` file to v1.3, if for any reason it doesn't work a backup of your ``config.json`` file will be saved as ``config.json.bak``.

v1.2 (*previous version*)
-------------------------------------------------------------------------------

Supported Platforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Chrome
* Android
* Firefox
* iOS
* Web

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
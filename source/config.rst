.. _config:

Config File Reference
================================================================================
``config.json`` is a JSON file which contains meta-data about your app. It determines how your app looks and functions by specifying which Javascript, image and HTML files are to be used.

Field summary
--------------------------------------------------------------------------------
Below is a template of a ``config.json`` file with links to a detailed description of each field.

.. parsed-literal::
    {
        ":ref:`config_version <field-config-version>`": 2,
        ":ref:`platform_version <field-platform-version>`": "v1.2",
        ":ref:`name <field-name>`": "My App",
        ":ref:`author <field-author>`": "Forger",
        ":ref:`version <field-version>`": "1.0",
        ":ref:`package_names <field-package_names>`": {
            "android": "com.example.app",
            "ios": "com.example.ios.app"
        },
        ":ref:`description <field-description>`": "My First Forge App.",
        ":ref:`icons <field-icons>`": {
            "android": {
                "16": "icon16.png",
                "32": "icon32.png",
                "48": "icon48-android.png"
            },
            "chrome": {
                "16": "icon16.png",
                "48": "icon48-chrome.png"
                "128": "icon128.png
            }
        },
        ":ref:`update_url <field-update_url>`": {
            "chrome": "url",
            "firefox": "url"
        },
        ":ref:`parameters <field-parameters>`": {},
        ":ref:`homepage <field-homepage>`": "http://example.com"",
        ":ref:`partners <field-partners>`": {},
        ":ref:`modules <field-modules>`": {
            "prefs": true
        },
    }


Fields
--------------------------------------------------------------------------------

This section includes more detailed information on the contents of each field, with links to other documentation where appropriate.

.. _field-config-version:

config_version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An internally used reference to keep track of changes to the Forge config file schema, you shouldn't need to change this property manually.

.. _field-platform-version:

platform_version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As the Forge platform grows and improves, we may deprecate and remove some functionality. To prevent these updates from breaking your app, use this field to specify the version of the Forge platform you wish to build on top of.

.. _field-name:

name
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This will be the name for your app, a short, descriptive name is recommended as in some situations long names may be cut off.

.. _field-author:

author
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This text will be displayed as the author or creator of the app, depending on the platform.

.. _field-version:

version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The version of your app. It must be formatted as up to three dot-separated numbers, e.g. ``1.1`` or ``0.99.9``.

.. _field-package_names:

package_names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default, we create a package name for your app, something like ``io.trigger.forge.appname*``. Although your users aren't going to see this value, it can sometimes be useful to be able to control it manually, for example when updating a previous app that wasn't built on Forge.

``package_names`` should be an object mapping a target name onto a package name, e.g.::

    "android": "com.example.my_app_name",
    "ios": "com.example.ios.app"

Currently, only ``android`` and ``ios`` are supported.

.. _field-description:

description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

A longer description of what your app does. This description may be displayed to users during and after installation, to let them know what the app does.

.. _field-icons:

icons
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

This part of the config allows you to define the icons to be used for your app. All icons are square, and must be placed in your ``src`` directory.

Define your desired icons with ``"size": "path"`` attributes, where ``size`` is the pixel height (and width) of the icon, and ``path`` is where the image has been placed under the ``src`` directory.

.. highlight:: js

You can specify different icons for different platforms as so::

    "android": {
        "16": "icon16.png",
        "32": "icon32.png",
        "48": "icon48-android.png"
    },
    "chrome": {
        "16": "icon16.png",
        "48": "icon48-chrome.png"
        "128": "icon128.png
    }

Here, Android and Chrome will share their 16x16 pixel icon, but use different 48x48 pixel icons.

The icons required for each platform are listed below:

* Android: 36px, 48px and 72px
* Chrome: 16px, 48px and 128px
* Firefox: 32px and 64px
* Internet Explorer: TODO
* iOS: 57px, 72px and 114px for home screen icons, 512px to be shown in iTunes.
* Safari: 32px, 48px and 64px

.. note:: If you specify *any* icons for a particular platform, you **must** specify all required icons!

.. _field-parameters:

parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Arbitrary extra configuration which will be available as ``forge.config.parameters`` in your JavaScript

.. _field-homepage:

homepage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Your website, or location of more information about this app.

.. _field-modules:

modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Enable and optionally configure optional modules. For more information check :ref:`our modules <modules>`.


.. _field-partners:

partners
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configuration for 3rd party integration. For more information check :ref:`our partners <partners>`.


Fields only used in browser apps
--------------------------------------------------------------------------------

.. _field-update_url:

update_url
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

URLs to check for application updates from::

    "update_url": {
        "chrome": "url",
        "firefox": "url"
    }
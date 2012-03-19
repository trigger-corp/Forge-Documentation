.. _config:

Config File Reference
================================================================================
``config.json`` is a JSON file which contains meta-data about your app. It determines how your app looks and functions by specifying which Javascript, image and HTML files are to be used.

Field summary
--------------------------------------------------------------------------------
Below is a template of a ``config.json`` file with links to a detailed description of each field.

.. parsed-literal::
    {
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
        ":ref:`launch_images <field-launch_images>`": {
            "iphone": "iphone.png",
            "iphone-retina": "iphone-retina.png",
            "ipad": "ipad.png",
            "ipad-landscape": "ipad-landscape.png",
            "android": "android.png",
            "android-landscape": "android-landscape.png"
        },
        ":ref:`permissions <field-permissions>`": ["tabs", "http://trigger.io/"],
        ":ref:`background_files <field-background_files>`": ["background.js"],
        ":ref:`activations <field-activations>`": [
            {
                ":ref:`patterns <field-activations-patterns>`": ["http://mail.google.com"],
                ":ref:`scripts <field-activations-scripts>`": ["gmail.js"],
                ":ref:`styles <field-activations-styles>`": ["gmail.css"],
                ":ref:`run_at <field-activations-runat>`": "start",
                ":ref:`all_frames <field-activations-allframes>`": false
            }
        ],
        ":ref:`orientations <field-orientations>`": {
            ":ref:`default <field-orientations_default>`": "any",
            ":ref:`iphone <field-orientations_iphone>`": "portrait",
            ":ref:`ipad <field-orientations_ipad>`": "landscape",
            ":ref:`android <field-orientations_android>`": "landscape",
        },
        ":ref:`browser_action <field-browser_action>`": {
            ":ref:`default_popup <field-default_popup>`": "popup.html",
            ":ref:`default_icon <field-default_icon>`": "my-default-icon.ico",
            ":ref:`default_icons <field-default_icons>`": {
                "firefox": "my-icon-for-firefox.ico"
            }
        },
        ":ref:`libs <field-libs>`": {
            "gmail": {}
        },
        ":ref:`update_url <field-update_url>`": {
            "chrome": "url",
            "firefox": "url"
        },
        ":ref:`logging <field-logging>`": {
            "level": ["DEBUG", "INFO", "WARNING", "ERROR", "CRITICAL"]
        },
        ":ref:`parameters <field-parameters>`": {},
        ":ref:`homepage <field-homepage>`": "http://example.com"",
        ":ref:`partners <field-partners>`": {},
        ":ref:`modules <field-modules>`": {
            "topbar": true
        },
    }


Fields
--------------------------------------------------------------------------------

This section includes more detailed information on the contents of each field, with links to other documentation where appropriate.

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

.. _field-permissions:

permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

.. _field-logging:

logging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The logging level defines the level of log messages which will appear in the console output for your app, see :ref:`the logging api docs <logging>` for more detail.

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

Enable and optionally configure optional modules.


.. _field-partners:

partners
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configuration for 3rd party integration. For more information check :ref:`our partners <partners>`.


Fields only used in mobile apps
--------------------------------------------------------------------------------

.. _field-launch_images:

launch_images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

Images to be displayed during launch as required on iOS, for further details see the `Apple documentation <http://developer.apple.com/library/ios/#documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/App-RelatedResources/App-RelatedResources.html#//apple_ref/doc/uid/TP40007072-CH6-SW12>`_.

On Android the image will be displayed centered on a black background while the first page is loading, as Android device sizes vary a pixel perfect loading image cannot be used. 

All 4 iOS images must be defined for any to be included in iOS builds. Both Android images must be defined for Android builds.

Properties and image sizes are:

* ``iphone``: 320x480px
* ``iphone-retina``: 640x960px
* ``ipad``: 768x1004px
* ``ipad-landscape``: 1024x748px
* ``android``
* ``android-landscape``

.. _field-orientations:

orientations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

This controls how your app will be displayed as the device is moved around. The default is to allow for any orientation, with the content being re-drawn as the screen is rotated.

.. _field-orientations_default:

You can limit this behaviour by specifying the desired supported orientations as ``orientations.default``, choosing from ``"any"``, ``"portrait"`` or ``"landscape"``.

.. _field-orientations_iphone:

.. _field-orientations_android:

.. _field-orientations_ipad:

You can further customise this behaviour by specifying orientation support for different devices, e.g. ``orientations.iphone`` and ``orientations.ipad``. For example::

  "orientations": {
    "default": "any",
    "iphone": "portrait",
    "ipad": "landscape"
  },

This configuration means

* by default, display your app in any orientation
* ... but on iPhones, only display your app in portrait mode, either way up
* ... and on iPads, your app will only use the landscape orientation
* ... on Android the default will apply and any orientation allowed by the device will be used

Fields only used in browser apps
--------------------------------------------------------------------------------

.. _field-background_files:

background_files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*. 

Browsers have the :ref:`concept of content scripts and background <extension-concepts>` files.
This field lists the files that should be included in background context.

.. _field-activations:

activations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

This field specifies when and how your foreground files will be embedded into pages. 
It is an array of objects with three required keys:

.. _field-activations-patterns:

.. _field-activations-scripts:

.. _field-activations-styles:


* ``patterns`` is an array of `Match Patterns <http://code.google.com/chrome/extensions/match_patterns.html>`_ which control on which URLs your app will activate
* ``scripts`` is an array of Javascript files which will be embedded
* ``styles`` is an array of CSS files which will be embedded

As well as an optional keys:

.. _field-activations-runat:

* ``run_at`` optionally defines when your included scripts will be added to the page, must be one of the following:

 * ``"start"`` scripts will be run immediately, potentially before the DOM is ready
 * ``"ready"`` scripts will run as soon as the DOM is ready
 * ``"end"`` (default) scripts will run at some point after the DOM is ready, with no guarantees as to whether or not ``window.onload`` will have fired yet or not.

.. _field-activations-allframes:

* ``all_frames`` optionally defines whether activations will be run in all frames or just the top level document, by default it is false.

.. important:: Safari only supports a single object in the activations array.

.. _field-browser_action:

browser_action
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

The ``browser_action`` configuration controls the appearance and function of toolbar icons in the browsers. With this directive, you can specify a HTML file which will be displayed when the button is clicked, a default button icon as well as platform-specific icons.

.. _field-default_popup:

.. _field-default_icon:

.. _field-default_icons:

* ``default_popup`` should refer to a local HTML file, included in your app, which will be displayed after the button is clicked; for more information, see :ref:`part I of the tutorial <tutorials-weather-tutorial-1-setting-up-the-UI>`
* ``default_icon`` should refer to a local image file, included in your app, to be used as the button icon
* ``default_icons`` allows you to override the ``default_icon`` icon, one platform at a time: the object keys should be one or more of ``chrome``, ``firefox``, ``safari`` or ``ie``


.. _field-libs:

libs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

For convenience, Forge comes with a number of libraries which you can choose to include with your app. The format of ``libs`` is an object, where the keys are the names of a library, and the values are extra configuration directives specific to each included library, e.g.::

    "libs": {
        "gmail": {}
    }

Currently, the only library you can enable here is called "gmail". The Forge gmail library gives the developer access to special functions which can interact with and manipulate the Gmail composition pane. This allows for a more flexible alternative to developing Gmail gadgets. Check the API section for :ref:`a detailed explanation of the Gmail library <api-gmail>`.

.. _field-update_url:

update_url
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

URLs to check for application updates from::

    "update_url": {
        "chrome": "url",
        "firefox": "url"
    }

.. _field-cs_options:

cs_options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

This array controls the details of behaviour for content scripts. Currently, only one option is available: ``frames``, e.g.::

    "cs_options": ["frames"]

When used, ``frames`` means that your extension may also activate inside iframes. When specified, if the ``src`` of an iframe matches one of your ``patterns``, your scripts and CSS files will be embedded in that iframe; not just in the top-level document.


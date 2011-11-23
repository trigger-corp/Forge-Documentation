.. _config:

Config file documentation
================================================================================

``config.json`` is a JSON file which contains meta-data about your app. It determines how your app looks and functions by specifying which Javascript, image and HTML files are to be used.

Field summary
--------------------------------------------------------------------------------

Below is a template of a ``config.json`` file with links to a detailed description of each field.

.. parsed-literal::

    {
        ":ref:`uuid <field-uuid>`": "ABCD-1234",
        ":ref:`platform_version <field-platform-version>`": "v1",
        ":ref:`name <field-name>`": "My App",
        ":ref:`author <field-author>`": "WebMynd",
        ":ref:`version <field-version>`": "1.0",
        ":ref:`description <field-description>`": "My First WebMynd App.",
        ":ref:`icons <field-icons>`": {
          "16": "icon16.png",
          "32": "icon32.png"
        },
        ":ref:`permissions <field-permissions>`": ["tabs", "http://webmynd.com/"],
        ":ref:`trigger <field-trigger>`": "document_end",
        ":ref:`background_files <field-background_files>`": ["background.js"],
        ":ref:`activations <field-activations>`": [
          {
            ":ref:`patterns <field-activations-patterns>`": ["http://mail.google.com"],
            ":ref:`scripts <field-activations-scripts>`": ["gmail.js"],
            ":ref:`styles <field-activations-styles>`": ["gmail.css"]
          }
        ],
        ":ref:`browser_action <field-browser_action>`": {
            ":ref:`default_popup <field-default_popup>`": "popup.html",
            ":ref:`default_icon <field-default_icon>`": "my-default-icon.ico",
            ":ref:`default_icons <field-default_icons>`": {
                "firefox": "my-icon-for-firefox.ico"
            }
        }
    }


Fields
--------------------------------------------------------------------------------

This section includes more detailed information on the contents of each file, with links to other documentation where appropriate.

.. _field-uuid:

uuid
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a unique identifier for your app, used internally by the Forge platform. This field must be left intact for your app to function properly.

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

The version of your app. It must be formatted as up to four dot-separated numbers, e.g. ``1.0.1`` or ``0.99.9.9``.

.. _field-description:

description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

A longer description of what your app does. This description may be displayed to users during and after installation, to let them know what the app does.

.. _field-icons:

icons
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

This part of the config allows you to define the icons to be used for your app.

Icons are defined as the size of the icon (the width and height as all icons are square) and the image to be used for the icon in your src directory. In order to provide high quality icons on all platforms you may need to provide a fair number of different icon sizes, the icons required for each platform are listed below:

* Android: 36px, 48px and 72px
* Chrome: 16px, 48px and 128px
* Firefox: 32px and 64px
* Internet Explorer: TODO
* iOS: 57px, 72px and 114px
* Safari: 32px, 48px and 64px

.. important:: Some platforms (such as Android and Safari) will not use any of your icons unless you specify icons of all the required sizes.

.. _field-permissions:

permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TODO

.. _field-trigger:

Fields only used in browser apps
--------------------------------------------------------------------------------

trigger
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

This field specifies when your browser app becomes active on a page. Permissible values are:

* ``"document_start"`` - your code is loaded and run before any other scripts on the page
* ``"document_end"`` - your code is loaded and run after the DOM has been constructed
* ``"document_idle"`` - your code is loaded and run before, or just after the ``window.onload`` event

These values range from activating the earliest to the latest.

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

This field specifies when and how your foreground files will be embedded into pages. It is an object with three required keys:

.. _field-activations-patterns:

.. _field-activations-scripts:

.. _field-activations-styles:

* ``patterns`` is an array of `Match Patterns <http://code.google.com/chrome/extensions/match_patterns.html>`_ which control on which URLs your app will activate
* ``scripts`` is an array of Javascript files which will be embedded
* ``styles`` is an array of CSS files which will be embedded

.. _field-browser_action:

browser_action
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*. *Browsers only*.

The ``browser_action`` configuration controls the appearance and function of toolbar icons in the browsers. With this directive, you can specify a HTML file which will be displayed when the button is clicked, a default button icon as well as platform-specific icons.

.. _field-default_popup:

.. _field-default_icon:

.. _field-default_icons:

* ``default_popup`` should refer to a local HTML file, included in your app, which will be displayed after the button is clicked; for more information, see :ref:`part I of the tutorial <weather-tutorial-1-setting-up-the-UI>`
* ``default_icon`` should refer to a local image file, included in your app, to be used as the button icon
* ``default_icons`` allows you to override the ``default_icon`` icon, one platform at a time: the object keys should be one or more of ``chrome``, ``firefox``, ``safari`` or ``ie``
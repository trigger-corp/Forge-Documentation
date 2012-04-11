.. _config:

Config File Reference
================================================================================
``config.json`` is a JSON file which contains meta-data about your app. It determines how your app looks and functions by specifying which Javascript, image and HTML files are to be used.

Field summary
--------------------------------------------------------------------------------
Below is a template of a ``config.json`` file with links to a detailed description of each field.

.. parsed-literal::
    {
        ":ref:`config_version <field-config-version>`": "2",
        ":ref:`platform_version <field-platform-version>`": "v1.3",
        ":ref:`name <field-name>`": "My App",
        ":ref:`author <field-author>`": "Forger",
        ":ref:`version <field-version>`": "1.0",
        ":ref:`description <field-description>`": "My First Forge App.",
        ":ref:`homepage <field-homepage>`": "http://example.com"",
        ":ref:`partners <field-partners>`": {},
        ":ref:`modules <field-modules>`": {}
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

.. _field-description:

description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Optional*.

A longer description of what your app does. This description may be displayed to users during and after installation, to let them know what the app does.

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

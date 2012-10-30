.. _native_plugins_including_resources:

.. role:: inline-html(raw)
   :format: html

Including resources
===================

Native code sometimes requires additional resources, such as layout or image
files. These work in slightly different ways on Android and iOS but can be
easily included in plugins for both.

Android
-------

When using the inspector project to develop your plugin, any required resources
should be added to the ``res/`` folder.

When you're ready to upload your plugin, these resources should also be copied
into ``android/res`` within your plugin folder.

.. important:: Resources must be accessed *dynamically* from your Java code:
    :inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeApp.html#getResourceId(java.lang.String, java.lang.String)">ForgeApp.getResourceId</a>`
    is a helper method which lets you access the ID for a named resource.

iOS
---

On iOS, any resources included in your plugin must be part of a bundle.

During development, 3rd party bundles can be added to the ForgeInspector
project. When you're ready to upload your plugin, copy the bundle to
``ios/bundles/`` in your plugin folder.

If you have resources such as images that you want to include in your plugin,
you must create your own bundle. The inspector project includes a
``ForgeModuleResources`` target which can be used to help with this:

1. All bundles must have a unique name - you can name your bundle by setting the
   ``Product Name`` for the ForgeModuleResources target.

.. image:: /_static/images/plugin-set-bundle-name.png

2. Add the required resources to the ``ForgeModule`` project and include them in
   the ``ForgeModuleResources`` target.
#. Use the named bundle to reference these resources from your native code -
   see `Accessing a Bundle's Contents <https://developer.apple.com/library/mac/#documentation/CoreFOundation/Conceptual/CFBundles/AccessingaBundlesContents/AccessingaBundlesContents.html>`_.
#. When building ``UniversalForgeModule`` your bundle will be output in the
   build folder: make sure to include this in ``ios/bundles/`` in your plugin
   folder before uploading.

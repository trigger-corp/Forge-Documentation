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

To include resources they must be placed in the ``plugin/android/res`` folder,
once there the inspector project can be updated and the resource files will be
included.

For more information about what kind of resources can be added to your plugin
and how they can be used with the Android SDK, see the `official Android docs
concerning App Resources`_.

.. _official Android docs concerning App Resources: http://developer.android.com/guide/topics/resources/index.html

.. important:: If you access resources using the R.java file you must include the trigger-gen folder in your jar file when exporting your code. This folder contains a specially generate R.java for plugins.

iOS
---

On iOS, any resources included in your plugin must be part of a bundle.

3rd party bundles can be included by placing the bundles in
``plugin/ios/bundles``. An inspector project update will then be required to
include them in the inspector for development

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

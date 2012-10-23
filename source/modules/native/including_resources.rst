.. _native_plugins_including_resources:

Including resources
===================

Native code sometimes requires additional resources, such as layout or image files. These work in slightly different ways on Android and iOS but can be easily included in plugins for both.

Android
-------

On Android any resources are added to the ``res/`` folder in the inspector app, to include these in plugin you should include anything you add to the ``res/`` folder to the ``android/res`` folder within your plugin.

iOS
---

In iOS any resources included in your plugin must be part of a bundle. 3rd party bundles can be placed in ``ios/bundles/`` in your plugin to be included, as well as in the ForgeInspector project during development.

Any resources not part of a 3rd party bundle must be added to your own bundle. To do this the inspector project includes a ForgeModuleResources target which can be used by for your plugin by:

* Naming the bundle - all bundles must have a unique name, you can name your bundle by setting the ``Product Name`` for the ForgeModuleResources target.

.. image:: /_static/images/plugin-set-bundle-name.png

* Including any resources in the ForgeModuleResources target within the ForgeModule project.
* Using the bundle with the name you created to reference any resources from the native code in your module.
* When building UniversalForgeModule your bundle will be output in the build folder, make sure to include this in ``ios/bundles`` in your plugin.
.. _native_plugins_external_libraries:

External libraries
==================

Often it is useful to include external libraries in your plugin, this can be done on both Android and iOS.

.. important:: Class names must be unique across all plugins and the core Forge
    app: this means multiple plugins cannot include the same libraries. In the
    future we will be supporting dependencies between plugins to allow shared
    libaries, until then if multiple plugins include the same libraries only one of
    them can be enabled for any individual app.

Android
-------

The easiest way to include libraries for Android is to copy them into the ``libs`` folder of the inspector project. Both Java and native libraries should work fine.

To include the library when your app is being built, make sure to copy any files from the ``libs`` folder of the inspector project to ``android/libs`` within your plugins folder.

If the code you wish to include is not as simple as including a jar then any code you include in the jar when exporting your plugin from eclipse will also be included in an app build with your plugin.

iOS
---

On iOS, there are both system frameworks made available by Apple, and 3rd party frameworks which you may wish to include in your app.

System frameworks
~~~~~~~~~~~~~~~~~

First, use the inspector project to test your plugin works with the system
framework - just add the framework to the inspector project in Xcode.

When using your plugin in a real app, to make the system framework is
available to your plugin, an :ref:`add_ios_system_framework build step
<native_plugins_native_build_steps>` must be added to link with the framework
at build time.

3rd party libraries/frameworks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are a number of different formats used to distribute 3rd party libraries for iOS, not all of which are directly compatibile with Forge, but all can be included in a plugin with minor changes:

* If the library is a .a file, simply include it in the ForgeModule project and add it to the ForgeModule target. If the library includes separate header files you can also add these to the ForgeModule project.
* If the library is a framework you will need to browse the contents of the framework and add the main framework file (which will be the name of the framework with no file extension) and any headers to the ForgeModule manually.
* If the framework contains any .bundle files you will need to add these to the ForgeInspector project and also include them in the plugin (see :ref:`native_plugins_including_resources`).

.. _native_plugins_external_libraries:

External libraries
==================

Often it is useful to include external libraries in your plugin, this can be
done on both Android and iOS.

.. important:: Class names must be unique across all plugins and the core Forge
    app: this means multiple plugins cannot include the same libraries. In the
    future we will be supporting dependencies between plugins to allow shared
    libaries; until then if multiple plugins include the same libraries only
    one of them can be enabled for any individual app.

Android
-------

While using the inspector project to develop your plugin, copy any required
libraries into the ``libs`` folder.

When you're ready to upload your plugin, copy the required libraries into
``android/libs`` within your plugin folder.

Both Java and native libraries are supported: native libraries should be placed
in a sub-folder to indicate the architecture they're built for - see
:ref:`native_plugins_the_basics_structure`.

If the library you want to include is distributed as unbuilt Java files, you
can include that code in your own plugin source tree and it will be exported as
part of the JAR file from Eclipse.

iOS
---

On iOS, there are two two types of external libraries: system frameworks made available by Apple, and 3rd party frameworks.

System frameworks
~~~~~~~~~~~~~~~~~

First, use the inspector project to test your plugin works with the system
framework - just add the framework to the inspector project in Xcode.

When you're ready to upload your plugin, to ensure the system framework is
available to your plugin in real apps, an :ref:`add_ios_system_framework build
step <native_plugins_native_build_steps>` must be added to link with the
framework at build time.

3rd party libraries/frameworks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are a number of different formats used to distribute 3rd party libraries
for iOS: not all of them are directly compatibile with Forge, but with some
minor changes they can all be included in a plugin:

* If the library is a .a file, simply include it in the ForgeModule project and
  add it to the ForgeModule target. If the library includes separate header
  files you can also add these to the ForgeModule project.
* If the library is a framework you will need to browse the contents of the
  framework and add the main framework file (which will be the name of the
  framework with no file extension) and any headers to the ForgeModule
  manually.
* If the framework contains any .bundle files you will need to add these to the
  ForgeInspector project and also include them in the plugin (see
  :ref:`native_plugins_including_resources`).

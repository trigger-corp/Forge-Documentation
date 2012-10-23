.. _native_plugins_the_basics:

The basics
==========

In order to allow developers to write native plugins we provide what we call inspector projects for both Android and iOS. These projects are Eclipse and Xcode projects that include the core library used by Forge, as well as an example plugin to get you started. This environment can be used as a sandbox to develop and compile your plugin.

Once you are happy with your plugin you can use the Toolkit to upload a compiled version with any additional files (detailed below) to the Forge build server. Once we have a copy of your plugin you can then add the plugin to your app through the app's config in the Toolkit.

Downloading the inspector projects
----------------------------------

Getting setup to develop native plugins is fairly simple, but there are some prerequistes you need to install.

Android
~~~~~~~

1. You will need Eclipse setup with the Android SDK, you can find details on how to install this on the Android developer site: http://developer.android.com/sdk/installing/index.html
2. Download the ForgeInspector project through your toolkit (you can find it on the Forge tab of any of your apps when you have plugins enabled).
3. Import this project into Eclipse

iOS
~~~

1. You will need a Mac running OS X
2. You will need Xcode 4.5, this is available as a free download in the OS X App Store
3. Download the ForgeInspector project through your toolkit (you can find it on the Forge tab of any of your apps when you have plugins enabled).
4. Open this project in Xcode.

At this point you can run the project, it includes an app which can list native methods exposed to Javascript and allows you to call them with sample data. It also includes a small example plugin called ``alert`` which allows you to show native alert style dialogs, and triggers an event in Javascript when the app is paused and resumed. It is probably a good idea to try out this plugin to get a feel for the layout of a plugin before you get started.

Structure of the inspector projects
-----------------------------------

General
~~~~~~~

* The assets folder contains files loaded into the webview, i.e. HTML/JS/CSS files.
* The ``assets/forge`` folder contains a prebuilt all.js which should not need to be modified.
* The ``assets/src`` folder contains a prebuilt Forge app designed for testing plugins, this allows you to run API methods from a simple web based GUI within the app. You can modify this app to suit your testing needs.

Android
~~~~~~~

* Plugins must contain a package ``io.trigger.forge.android.modules.<plugin>`` where ``<plugin>`` is the plugin name
* This package can contain an API.java file which is the API exposed to Javascript, see API methods.
* It can also contain an EventListener.java, to listen for native events, see Events.
* An example plugin is included in ``io.trigger.forge.android.modules.alert``
* The file ``res/values/strings.xml`` contains a list of modules which will be enabled, by default this includes the ``alert`` example plugin, and the built in ``inspector`` module which can be used to list API methods from Javascript. You must add your package name to this file if you want its EventListeners and API methods to be loaded.

iOS
~~~

The iOS inspector project should look something like this:

.. image:: /_static/images/plugin-ios-inspector.png

The ForgeModule subproject is used to contain the code and resources for your plugin, and the ForgeInspector outer-project is the sandbox you can run and test your plugin in before packaging it up to send to Trigger.io.

* There is no namespacing in Objective-C, you can create files in any structure you like in the ForgeInspector project.
* Files to be included in the plugin build should be in the ForgeModule project and included in the ForgeModule target.
* Plugins can include a ``<plugin>_API.m`` file which is the API exposed to Javascript, see API Methods.
* An example plugin is included in ``ForgeModule/alert/alert_API.m``
* The file ``app_config.json`` contains a list of modules which will be enabled, by default this includes the ``alert`` example plugin, and the built in ``inspector`` module which can be used to list API methods from Javascript

Structure of a plugin
---------------------

In order to upload a plugin you must put the files that make up a plugin, along with a manifest for the plugin in a particular structure in a folder. To help you get started the toolkit can create a template folder for you when you create your plugin.

Plugins take the following structure::

    manifest.json                       - Contains the basic properties for your plugin
    android/                            - Folder containing all android related files
            plugin.jar                  - Built Android code
            build_steps.json            - Android build steps, see native build steps
            res/                        - Android resource files, see including resources
                values/
                       myvalues.xml
            libs/                       - Android libraries
                 mysdk.jar
                 arm/
                     mynativesdk.so
    ios/                                - Folder containing iOS related files
        plugin.a                        - Built iOS plugin
        build_steps.json                - iOS build steps
        bundles/                        - iOS bundles (resources) to include
                myplugin.bundle
                mysdk.bundle

Testing your plugin
-------------------

An inspector app is included which allows you to view all available API methods and call them. You can modify this app in the ``assets/src`` folder to test your plugin as you like. Simply running the inspector project through Xcode or Eclipse should start the app in a simulator or on a connected device for you to test your code.

Building/packaging your plugin 
------------------------------

Android
~~~~~~~

To build and export your plugin to be included in an actual Forge app simply right click the ``src`` folder and choose export. Use the wizard to export the contents of the folder as a jar, and save that jar as ``android/plugin.jar`` in your plugin folder.

iOS
~~~

To build and export your plugin to be included in an actual Forge app choose the ``UniversalForgeModule`` target and press run. A file ``build/plugin.a`` should appear in the ForgeInspector folder, save that file as ``ios/plugin.a`` in your plugin folder.
.. _native_plugins_ios:

iOS native plugins
==================

Getting setup
-------------

Getting setup to develop native plugins is fairly simple, but there are some prerequistes you need to install:

1. You will need Xcode 4.5, this is available as a free download in the OS X App Store
2. Download the ForgeInspector project through your toolkit (you can find it on the Forge tab of any of your apps when you have plugins enabled).
3. Open this project in Xcode.

At this point you can run the project, it includes an app which can list native methods exposed to Javascript and allows you to call them with sample data. It also includes a small example plugin called ``alert`` which allows you to show native alert style dialogs. It is probably a good idea to try out this plugin to get a feel for the layout of a plugin before you get started.

Structure of the app
--------------------

* There is no namespacing in Objective-C, you can create files in any structure you like in the ForgeInspector project.
* Files to be included in the plugin should have target membership of both ``ForgeInspector`` and ``ForgeModule``.

.. image:: /_static/images/ios_native_plugin_0.png

* Plugins should include a ``<plugin>_API.m`` file which is the API exposed to Javascript
* An example plugin is included in ``alert/alert_API.m``
* The file ``app_config.json`` contains a list of modules which will be enabled, by default this includes the ``alert`` example plugin, and the built in ``inspector`` module which can be used to list API methods from Javascript
* The assets folder contains files loaded into the webview, i.e. HTML/JS/CSS files.

  * The ``assets/forge`` folder contains a prebuild all.js which should not need to be modified
  * The ``assets/src`` folder contains a prebuilt Forge app designed for testing plugins, this allows you to run API methods from a simple web based GUI within the app. You can modify this app to suit your testing needs.

Structure of an API method
--------------------------

An example API method is included in the alert plugin, the easiest way to get started is to look at that method.

* API methods exposed to Javascript are ``+ (void)`` methods in ``<plugin>_API.m``
* The first parameter to API methods is a ``ForgeTask`` object, which contains information about the task as well as helper methods to complete the task and to return a response.
* Additional parameters must be NSString, NSNumber, NSDictionary or NSArray, the name of the parameter will be used to extract the argument from the javascript parameters object. Type checking is not performed on iOS.
* To finish an API method call ``[task success:returnValue]`` or ``[task error:returnValue]``. The returnValue will be returned to Javascript.
* From Javascript API methods are called using:
  ``forge.internal.call("plugin.method", {params: object}, function () { //success }, function () { //error });``
 
  * ``method`` is the Objective-C method name to call
  * ``{params: object}`` is a dictionary of parameters to pass through, any parameters named in the method will be passed directly to the method, any other parameters can be accessed through ``[ForgeTask params]``.
  * The last two parameters are the success and error callbacks
  
Testing your plugin
-------------------

Select the ForgeInspector target in Xcode and you should be able to run the app on either the simulator or an iOS device. You can modify the prebuilt app in the ``assets/src`` folder to test your plugin.

Building/packaging your plugin
------------------------------

To build and export your plugin to be included in an actual Forge app choose the ``UniversalForgeModule`` target and press run. A file ``build/libForgeModule.a`` should appear in the ForgeInspector folder, upload this to Forge to include it in your app.

List of classes
---------------

* ``ForgeTask`` - Holds information about an API method call and provides helper functions to complete the task and to respond either success or error.
* ``ForgeLog`` - Allows log messages to be outputs

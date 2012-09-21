.. _native_plugins_android:

Android native plugins
======================

Getting setup
-------------

Getting setup to develop native plugins is fairly simple, but there are some prerequistes you need to install:

1. You will need Eclipse setup with the Android SDK, you can find details on how to install this on the Android developer site: http://developer.android.com/sdk/installing/index.html
2. Download the ForgeInspector project through your toolkit (you can find it on the Forge tab of any of your apps when you have plugins enabled).
3. Import this project into Eclipse

At this point you can run the project, it includes an app which can list native methods exposed to Javascript and allows you to call them with sample data. It also includes a small example plugin called ``alert`` which allows you to show native alert style dialogs. It is probably a good idea to try out this plugin to get a feel for the layout of a plugin before you get started.

Structure of the app
--------------------

* Plugins must contain a package ``io.trigger.forge.android.modules.<plugin>`` where ``<plugin>`` is the plugin name
* This package should contain an API.java file which is the API exposed to Javascript
* An example plugin is included in ``io.trigger.forge.android.modules.alert``
* The file ``res/values/strings.xml`` contains a list of modules which will be enabled, by default this includes the ``alert`` example plugin, and the built in ``inspector`` module which can be used to list API methods from Javascript
* The assets folder contains files loaded into the webview, i.e. HTML/JS/CSS files.

  * The ``assets/forge`` folder contains a prebuilt all.js which should not need to be modified
  * The ``assets/src`` folder contains a prebuilt Forge app designed for testing plugins, this allows you to run API methods from a simple web based GUI within the app. You can modify this app to suit your testing needs.

Structure of an API method
--------------------------

An example API method is included in the alert plugin, the easiest way to get started is to look at that method.

* API methods exposed to Javascript are ``public static void`` methods in API.java
* The first parameter to API methods is ``ForgeTask``, which contains information about the task as well as helper methods to complete the task and to return a response.
* Additional parameters must be String, long, int, double, JSONArray or JSONObject and must have a ``@ForgeParam`` annotation.
* ``@ForgeParam`` annotations pass properties from Javascript directly to parameters in the API method, after checking they exist and are the right type.
* To finish an API method call ``task.success(returnValue)`` or ``task.error(returnValue)``. The returnValue will be returned to Javascript.
* From Javascript API methods are called using:
  ``forge.internal.call("plugin.method", {params: object}, function () { //success }, function () { //error });``
  
  * ``method`` is the Java method name to call
  * ``{params: object}`` is a dictionary of parameters to pass through, any parameters declared with ``@ForgeParam`` will be passed directly to the function, any other parameters can be accessed through ``ForgeTask.params``.
  * The last two parameters are the success and error callbacks

Testing your plugin
-------------------

Pressing run in eclipse should run the Android app which you can then test your plugin in, by default an inspector app is included which allows you to view all available API methods and call them. You can modify this app in the ""assets/src"" folder to test your plugin as you like.

Building/packaging your plugin
------------------------------

To build and export your plugin to be included in an actual Forge app simply right click the ``src`` folder and choose export. Use the wizard to export the contents of the folder as a jar, and upload that jar to Forge through the plugins management interface in the Toolkit.

List of classes
---------------

* ForgeTask - Holds information about an API method call and provides helper functions to complete the task and to respond either success or error.
* ForgeLog - Allows log messages to be output
* ForgeParam - Annotation to allow additional parameters in API methods
* JSONObject - Object representing a JSON dictionary
* JSONArray - Object representing a JSON array

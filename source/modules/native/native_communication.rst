.. _native_plugins_native_communication:

.. role:: inline-html(raw)
   :format: html

Communicating with native code
==============================

When making native API calls or triggering events it is useful to send more than just a string as data between the JavaScript and native code (in both directions).

On both Android and iOS you are able to send either simple pieces of data (numbers or strings) or JavaScript style objects and arrays in both directions. In JavaScript this means you can send any JSON serializable data to native, and you will always recieve back JSON parsed variables.

Android
-------

To encode and decode this JSON data in Java we use the Gson library. This provides a fast way of working with JSON with a simple and clear API. When working on Android you should keep the following in mind:

* When returning data to JavaScript it should be a :inline-html:`<a href="../../_static/native/android/reference/com/google/gson/JsonElement.html">JsonElement</a>`.

  * Simple types can be converted to a ``JsonElement`` using the :inline-html:`<a href="../../_static/native/android/reference/com/google/gson/JsonPrimitive.html">JsonPrimitive</a>` constructor: ``new JsonPrimitive("My string")`` or ``new JsonPrimitive(50)``.
  * More complex types can be created using :inline-html:`<a href="../../_static/native/android/reference/com/google/gson/JsonObject.html">JsonObject</a>` and :inline-html:`<a href="../../_static/native/android/reference/com/google/gson/JsonArray.html">JsonArray</a>`.
  * ``ForgeTask.success`` and ``ForgeApp.event`` will also directly accept a ``String`` and create the ``JsonElement`` for you.

* ``ForgeTask.params`` is of type :inline-html:`<a href="../../_static/native/android/reference/com/google/gson/JsonObject.html">JsonObject</a>`. To read the string ``test`` from ``{"test":"My Data"}`` sent from Javascript the following code could be used ``task.params.get("test").getAsString()``.
* If accepting parameters directly using the :inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeParam.html">ForgeParam</a>` annotation then the types ``JsonObject`` and ``JsonArray`` must be used rather than ``JSONObject`` and ``JSONArray``.
* ``null`` passed to and from JavaScript is represented by ``JsonNull.INSTANCE``.

iOS
---

On iOS we use JSONKit to encode and decode JSON data. When working on iOS you should keep the following in mind:

* JSONKit maps JSON on to the familiar NSNull, NSString, NSNumber, NSArray and NSDictionary objects: any time you return data to JavaScript you should return one of these types. Any time you receive data from Javascript, you should expect one of these types.
* JavaScript booleans are encoded as NSNumber using ``[NSNumber numberWithBool:YES/NO]``
.. _native_plugins_api_methods:

.. role:: inline-html(raw)
   :format: html

Exposing native APIs to Javascript
==================================

One use of native plugins is to expose to Javascript a number of API methods
that run native code. To facilitate this, Forge provides a structure to
simplify communication between Javascript and native code.

.. important:: API Methods are always asynchronous: this means you provide a
    callback in Javascript which will be called with the result, and other
    Javascript code may excute while waiting for the result. This also means in
    native code you can perform tasks that don't return immediately without
    blocking Javascript execution.

Javascript
----------

To make an API call from Javascript the following code is used::

    forge.internal.call(
        'alert.show',
        {text: 'Test'},
        function () { alert('Success!') },
        function (e) { alert('Error: '+e.message)}
    )

The ``forge.internal.call`` method sends a message to native code, it takes 4
parameters:

* ``alert.show`` is a string representing the native method which will be
  called: in this case the method ``show`` will be called from the plugin
  ``alert``. See the Android and iOS sections below for more detail on how the
  native method will be found.
* The second parameter is an object containing data to be passed back to the
  method. Top level properties in this object can be passed directly to
  parameters in the method (see below for details). This object must be JSON
  serializable.
* The third parameter is a success callback, which may be called with data
  returned from native code.
* The forth parameter is an error callback, this may also be called with data,
  it is conventional to return a human readable description of the error in the
  property ``message`` of the returned object.

To expose an API similar to standard Forge modules you can include JavaScript code with your plugin by placing it in ``javascript/plugin.js`` in your plugin directory. to expose the ``alert.show`` method above you could use code such as::

    forge.alert = {
        show: function (text, success, error) {
            forge.internal.call('alert.show', {text: text}, success, error);
        }
    };

Android
-------

To expose API methods in Android they must be in API.java in the package
``io.trigger.forge.android.modules.<plugin>`` where ``<plugin>`` is your plugin
name.

To explain the structure of an Android API method we can look at the
``alert.show`` method included in the inspector project:

.. code-block:: java

    public static void show(final ForgeTask task, @ForgeParam("text") final String text) {
        if (text.length() == 0) {
            // Error if there is no text to show
            task.error("No text entered");
            return;
        }
        AlertDialog.Builder builder = new AlertDialog.Builder(ForgeApp.getActivity());
        builder.setMessage(text).setCancelable(false).setPositiveButton("Ok",
            new DialogInterface.OnClickListener() {
                public void onClick(DialogInterface dialog, int which) {
                    task.success();
                }
            }
        );
        AlertDialog alert = builder.create();
        alert.show();
    }

Firstly, looking at the method signature:

* All exposed API methods should be ``public static void`` methods.
* The first parameter is always a
  :inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeTask.html">ForgeTask</a>`
  object, which contains information about the task as well as helper methods
  to complete the task and to return a response.
* Additional parameters must be ``String``, ``long``, ``int``, ``double``,
  ``JsonArray`` or ``JsonObject`` and must have a ``@ForgeParam`` annotation.
* :inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeParam.html">ForgeParam</a>`
  annotations pass properties with the given name from Javascript directly to
  parameters in the API method, after checking they exist and are the right
  type.
* Parameters do not need to be specified and the full :inline-html:`<a href="../../_static/native/android/reference/com/google/gson/JsonObject.html">JsonObject</a>` passed
  from Javascript can be accessed through ``task.params``.

Most of the method body is code to display the alert dialog in Android, the important lines to notice related to Forge are:

* ``task.error("No text entered");`` - Returns the string given to the
  error callback in Javascript.
* ``task.success();`` - Calls the success callback in Javascript with no
  arguments.
* We can see the success method is only called when the alert dialog button is
  clicked, which means it happens asynchronously: this is not a problem.

All API methods should call ``task.error()`` or ``task.success()`` **exactly
once**: if a method needs to return values to Javascript multiple times then
events should be used.

iOS
---

API methods are exposed in iOS by creating a class called ``<plugin>_API``
within the ForgeModule project where ``<plugin>`` is your plugin name.

The structure of an API method can be seen in the example included in the
inspector project:

.. code-block:: objective-c

    + (void)show:(ForgeTask*)task text:(NSString *)text {
        if ([text length] == 0) {
            [task error:@"You must enter a message"];
            return;
        }
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Alert"
                                                        message:text
                                                       delegate:nil
                                              cancelButtonTitle:@"OK"
                                              otherButtonTitles:nil];
        [alert show];
        [task success:nil];
    }

The method signature defines the API method:

* All exposed API methods are ``+ (void)`` methods.
* The name of the exposed method is taken up to the first ``:``, so in this
  case is ``show``
* The first parameter to API methods is a
  :inline-html:`<a href="../../_static/native/ios/Classes/ForgeTask.html">ForgeTask</a>`
  object, which contains information about the task as well as helper methods
  to complete the task and to return a response.
* Additional parameters must be ``NSString``, ``NSNumber``, ``NSDictionary`` or
  ``NSArray``, the name of the parameter will be used to extract the argument
  from the javascript parameters object. Type checking is not performed on iOS.
* Any parameters not specified in the signature can be accessed through
  ``task.params``

The method body contains the following Forge specific features:

* ``[task error:@"You must enter a message"];`` - Returns a string to the error
  callback in Javascript
* ``[task success:nil];`` - Returns no parameters to the success callback in
  Javascript

All API methods should call ``[task error:]`` or ``[task success:]`` exactly
once.

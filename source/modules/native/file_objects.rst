.. _native_plugins_file_objects:

.. role:: inline-html(raw)
   :format: html

Working with files
==================

Forge plugins will often want to consume or produce files (or both). To make this easy Forge has a ForgeFile object which can be passed efficiently between plugins and between native and JavaScript code.

Javascript
----------

ForgeFile objects can be represented as simple JavaScript objects. These objects must contain a ``uri`` which references an actual file that either Forge or a loaded plugin will be able to resolve at a later point. They should also contain a ``name`` and a ``mimeType`` if sensible values for these are known. Some file objects will contain additional properties such as ``width`` and ``height`` which may be used when processing the file.

The ``file`` module has a number of methods which accept file objects.

In the inspector project it can be useful to create file objects to test with. Calling ``forge.inspector.getFixture("plugin", "file.png")`` will return a file object for the file in ``src/fixtures/plugin/file.png``. In future versions of the inspector projects the fixtures folder will be automatically populated, for now you will have to create it and add any files you want to test with manually.

Android
-------

Receiving from JavaScript
~~~~~~~~~~~~~~~~~~~~~~~~~

When receiving a file from JavaScript it will be of type JsonObject, this can be passed into the ForgeFile constructor to access various helper fuctions for the file. For example::

    ForgeFile file = new ForgeFile(ForgeApp.getActivity(), task.params.get("file"));
    byte[] fileData = null;
    try {
        fileData = file.data();
    } catch (IOException e) {
        // handle properly
    }

Further details on the ForgeFile class in Android can be found in the API docs: :inline-html:`<a href="../../_static/native/android/reference/io/trigger/forge/android/core/ForgeFile.html">ForgeFile</a>`

Returning to JavaScript
~~~~~~~~~~~~~~~~~~~~~~~

To return a file to JavaScript (which can then be used with other modules, such as forge.request.ajax) a JsonObject with the appropriate properties must be constructed and returned. For example::

    JsonObject file = new JsonObject();
    file.addProperty("uri", "file:///data/path/to/file");
    task.success(file);

iOS
---

Receiving from JavaScript
~~~~~~~~~~~~~~~~~~~~~~~~~

When receiving a file from JavaScript it will be of type NSDictionary, this can be passed into the ForgeFile constructor to access various helper fuctions for the file. For example::

    ForgeFile* file = [[ForgeFile alloc] initWithFile:[task.params objectForKey:@"file"]];
    NSString* fileURL = [file url];

Further details on the ForgeFile class in iOS can be found in the API docs: :inline-html:`<a href="../../_static/native/ios/Classes/ForgeFile.html">ForgeFile</a>`

Returning to JavaScript
~~~~~~~~~~~~~~~~~~~~~~~

To return a file to JavaScript (which can then be used with other modules, such as forge.request.ajax) an NSDictionary with the appropriate properties must be constructed and returned. For example::

    NSDictionary* file = @{@"uri": @"/path/to/file"};
    [task success:file];

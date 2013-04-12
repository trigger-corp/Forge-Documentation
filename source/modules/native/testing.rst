.. _native_plugins_testing:

Testing your plugin
===================

As well as allowing you to directly call exposed API methods, the Inspector project will run tests you include with your plugin. These tests are written in JavaScript, using QUnit, and are split into automated and interactive sections. To run the tests simply press the appropriate button when running the Inspector project.

Automated tests
---------------

To include automated tests you should create a file ``tests/automated.js`` in your ``plugin`` folder: it is important that these tests complete without requiring user input as we may run them automatically to check compatibility with new platform versions. Test as much of your API as possible in these tests, so that we can give you early warning about incompatibility with new platform versions and other plugins.

An example automated test (from the ``prefs`` module) could be::

    asyncTest("Set and get a pref (Number)", 1, function() {
        var pref = "test"+Math.random();
        var value = Math.random();
        forge.prefs.set(pref, value, function () {
            forge.prefs.get(pref, function (newValue) {
                equal(newValue, value, "Preference value which was set");
                start();
            });
        });
    });

Further documentation on available QUnit methods is available at: http://api.qunitjs.com/.

Interactive tests
-----------------

Sometimes tests require user interaction - in this case you should include them in ``tests/interactive.js`` in your ``plugin`` folder. These tests will never be run automatically, but placing them here is a good way for you to be able to test the functionality of your plugin as you develop it.

A helper function ``askQuestion(question, answers)`` is provided to make it easier to prompt the user for input: ``question`` is the question to ask, and ``answers`` is a mapping of answers to callback functions.

An example interactive test (this time taken from the ``barcode`` module) could be::

    asyncTest("Scan barcode", 1, function() {
        askQuestion("Does this device have a camera? If yes when prompted scan a barcode", {
            Yes: function () {
                forge.barcode.scanWithFormat(function (barcode) {
                    askQuestion("Is this your barcode: "+barcode.value+" and was it a: "+barcode.format, {
                        Yes: function () {
                            ok(true, "User claims success");
                            start();
                        },
                        No: function () {
                            ok(false, "User claims failure");
                            start();
                        }
                    });
                }, function (e) {
                    ok(false, "API call failure: "+e.message);
                    start();
                });
            },
            No: function () {
                ok(true, "No camera");
                start();
            }
        });
    });


Fixtures
--------

If you need to use additional resources (such as an image file) as part of your test, you can place them in the ``tests/fixtures`` folder in your plugin. These files will be included in ``src/fixtures/<plugin name>/`` when you update the Inspector app.

If your plugin has an API which accepts a ForgeFile object as described in :ref:`native_plugins_file_objects`, it can be useful to create file objects to test with. Calling ``forge.inspector.getFixture("plugin", "file.png")`` will return a ForgeFile object for the fixture "file.png".

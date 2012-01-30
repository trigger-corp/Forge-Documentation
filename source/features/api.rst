.. _forge-features-api:

Using API methods
=================

Most API methods provided by Forge operate asynchronously (exceptions include ``forge.is`` methods and ``forge.tools.UUID``). This means the result of the method is not returned immediately; instead you must provide a function which will be called with the result. Care must therefore be taken when using the methods, as the order in which code is executed can be less obvious.

Here is a simplified example:

::

    var url;
    forge.tools.getURL("mypage.html", function (myUrl) {
        url = myUrl;
    });
    alert(url);

In this code the alert might be undefined as you cannot be sure the callback would be fired before the next line of code. Instead it would be better to say:

::

    var url;
    forge.tools.getURL("mypage.html", function (myUrl) {
        url = myUrl;
        alert(url);
    });

The different callbacks which appear in Forge API methods are described below.

Callbacks
~~~~~~~~~

Asynchronous API methods will always have the last two parameters they take as callback functions. The first of which will either be ``success`` or ``callback`` and the second will always be ``error``. The way these functions are called is described below.

``success``
-----------

The most commonly used callback is the ``success`` callback, this is the penultimate parameter to most Forge API methods. The ``success`` callback can be called with a variety of paramters (including none at all), depending on the particular method.

The ``success`` callback will only ever be called once, and will only be called if the API method completes successfully.

``callback``
----------------

The ``callback`` callback is similar to ``success`` in that it appears as the penultimate parameter - however, unlike the ``success`` callback, it may be called multiple times. An example of its use it adding a listener to a button being clicked, as the button can be clicked multiple times the callback may be called multiple times.

.. _forge-features-api-error:

``error``
-----------

The ``error`` callback is always the final parameter passed to a method. The error callback will always be called with exactly one paramter, which will be an object containing several properties.

The returned object will always contain:

* A ``message`` property, which is a printable, human readable string describing the error which has occurred.

It will usually also contain:

* A ``type`` property, this will be one of the following strings and can be used to determine what type of error occurred and how to appropriately deal with it.
 * ``"BAD_INPUT"`` - returned when an API is given invalid parameters, this kind of error should be eliminated before releasing your app.
 * ``"UNEXPECTED_FAILURE"`` - returned when an unexpected error causes the API call to fail, this generally means an error in the forge API and we would be grateful if you could report this kind of error to us.
 * ``"EXPECTED_FAILURE"`` - returned when an expected situation occurs which means the API call is not successful, examples could be a user cancelled action or a timeout. These types of errors should be handled appropriately within your application.
 * ``"UNAVAILABLE"`` - returned when an API method is currently unavailable, this could mean unavailable on the current platform, in the current context, or at this time (i.e. if there is no Internet connection). Your application may also expected some errors of this type. Also returned for non-existant API calls.
* A ``subtype`` property which will give a more precise description of the error than the ``type``, the strings which this may contain are documented with each API method.

It may also contain additional properties which are relevant to the API method, these properties will be documented per method in the API reference.

When errors happen the message property will always be logged by Forge, whether a callback handler exists or not.
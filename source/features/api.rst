.. _forge-features-api:

Using API methods
=================

Most API methods provided by Forge operate asynchronously (exceptions include ``forge.is`` methods and ``forge.tools.UUID``). This means the result of the method is not returned immediately, instead you must provide a function which will be called with the result. Care must therefore be taken when using the methods, as the order in which code is executed can be less obvious.

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
-----------

The ``callback`` callback is similar to ``success`` in that it appears as the penultimate parameter, however unlike the ``success`` callback it may be called multiple times. An example of its use it adding a listener to a button being clicked, as the button can be clicked multiple times the callback may be called multiple times.

``error``
-----------

The ``error`` callback is always the final paramter passed to a method. The error callback will always be called with exactly one paramter, which will be an object which is guaranteed to contain a ``message`` property, with a human readable description of the error which has occurred. Other properties may be available depending on the API method being called. When errors happen the message property will always be logged by Forge, whether a callback handler exists or not.
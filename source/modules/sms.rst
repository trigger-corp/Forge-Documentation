.. _modules-sms:

``sms``: SMS messaging
======================

The ``forge.sms`` namespace allows you to prompt the user to send SMS messages from your app.

Config
------

The ``sms`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "sms": true
        }
    }

API
---

``send``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Send an SMS message, optionally with one or more recipients and a message pre-filled in.

Example::

   forge.sms.send({
     body: "Hello, World!",
     to: ["123457869", "328592835"]
   }, function () {
     alert("Message sent");
   });

.. js:function:: sms.send(params, success, error)

    :param function() params: Data to pre-fill SMS message with, contains ``body`` which is the content of the message, and ``to`` as either a string or array of phone numbers to send to.
    :param function() success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

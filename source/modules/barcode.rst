.. _modules-barcode:

``barcode``: Barcode / QR Code scanner
=======================================

The ``forge.barcode`` namespace allows the user to scan a barcode using the devices camera and returns its content

Config
------

The ``barcode`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "barcode": true
        }
    }

API
---

``scan``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Show a UI that allows the user to scan a barcode and return its value

Example::

   forge.barcode.scan(function (value) {
       alert("You scanned: "+value);
   });

.. js:function:: barcode.scan(success, error)

    :param function(value) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

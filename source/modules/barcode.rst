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
**Platforms: iOS, Android**

Show a UI that allows the user to scan a barcode and return its value

Example::

   forge.barcode.scan(function (value) {
       alert("You scanned: "+value);
   });

.. js:function:: barcode.scan(success, error)

    :param function(value) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur


``scanWithFormat``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: iOS, Android**

Show a UI that allows the user to scan a barcode and return its value and type.

Example::

    forge.barcode.scanWithFormat(function (barcode) {
      alert('You scanned a '+barcode.format+': '+barcode.value);
    });

.. js:function:: barcode.scanWithFormat(success, error)

    :param function(barcode) success: callback to be invoked when no errors occur - ``barcode`` will contain ``format`` and ``value`` keys, where ``format`` is the barcode type as returned by `ZXing <https://github.com/zxing/zxing>`_
    :param function(content) error: called with details of any error which may occur

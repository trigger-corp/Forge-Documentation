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

``scanWithFormat``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Show a UI that allows the user to scan a barcode and return its value along with the barcode format.

The format will be one of: ``AZTEC``, ``CODABAR``, ``CODE_39``, ``CODE_128``, ``DATA_MATRIX``, ``EAN_8``, ``EAN_13``, ``ITF``, ``PDF_417``, ``QR_CODE``, ``RSS_14``, ``RSS_EXPANDED``, ``UPC_A``, ``UPC_E``, ``UPC_EAN_EXTENSION``, ``UNKNOWN``.

Example::

   forge.barcode.scanWithFormat(function (result) {
       alert("You scanned: "+result.value);
       alert("The barcode type was: "+result.format);
   });

.. js:function:: barcode.scanWithFormat(success, error)

    :param function({value: barcodeValue, format: barcodeFormat}) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur

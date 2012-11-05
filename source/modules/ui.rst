.. _modules-ui:

``ui``: Native UI enhancements
==============================

This module includes miscellaneous native UI enhancements. This currently consists of enhancement to date, time and datetime form elements on Android.


Config
------

The ``ui`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "ui": true
        }
    }

API
---

``enhanceInput``
~~~~~~~~~~~~~~~~

**Platform: Android**

This method can be used to enhance a specific or set of specific input elements, when called any input elements of type ``date``, ``time`` or ``datetime`` matching the given selector will be updated to show a native date picker when the user taps on them. The value the user selects will be inserted into the input element so it can be treated as normal by other Javascript. The input element will also be disabled to prevent other user input into the field.

.. js:function:: ui.enhanceInput(selector)

    :param string selector: Any input elements of type date, time or datetime matching this selector will be enhanced.


``enhanceAllInputs``
~~~~~~~~~~~~~~~~~~~~

**Platform: Android**

This method will enhance all appropriate input elements currently in the DOM.

.. js:function:: ui.enhanceAllInputs()




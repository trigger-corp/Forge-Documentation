.. _modules-prefs:

``prefs``: Preferences
======================

Preferences are used to save state in your extension. State is persisted between restarts and is consistent across all parts of your app.

Config
------

The ``prefs`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "prefs": true
        }
    }

API
---

.. _api-prefs-get:

``get``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. js:function:: prefs.get(name, success, error)

    :param string name: the name of the preference you want to query
    :param function(value) success: will be invoked as the preference value as its only parameter
    :param function(content) error: called with details of any error which may occur

**Platforms: All**

If the preference has not been set (with :ref:`api-prefs-set`), and there is no default value for this preference, ``null`` is returned.

.. _api-prefs-set:

``set``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.set(name, value, success, error)

    :param string name: the name of the preference you want to save
    :param value: the value to save
    :param function() success: callback to be invoked when no errors occurs
    :param function(content) error: called with details of any error which may occur

The preference value given here will override a default value (if one was given).

``clear``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.clear(name, success, error)

    :param string name: the name of the preference to un-set
    :param function() success: a callback to be invoked (with no arguments) when the operation is complete
    :param function(content) error: called with details of any error which may occur

Un-sets the given preference name, so that future calls to :ref:`api-prefs-set` will return ``undefined`` (or the default preference value, if given).

``clearAll``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.clearAll(success, error)

    :param function() success: a callback to be invoked (with no arguments) when the operation is complete
    :param function(content) error: called with details of any error which may occur

Un-sets all preference names, so that calls to :ref:`api-prefs-set` will return ``undefined`` (or the default value for a preference, if given).

``keys``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.keys(success, error)

    :param function(keysArray) success: invoked with an array of the set key names as its only argument
    :param function(content) error: called with details of any error which may occur

Find which preferences have been set.
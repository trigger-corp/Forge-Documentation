.. _preferences:

Preferences: ``forge.prefs``
================================================================================

Preferences are used to save state in your extension, state is persisted between restarts and is consistent across all parts of your app.

.. _api-prefs-get:

``get``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. js:function:: prefs.get(name, callback, error)

    :param string name: the name of the preference you want to query
    :param function callback: will be invoked as the preference value as its only parameter
    :param function error: callback to be invoked when an error occurs

**Platforms: All**

If the preference has not been set (with :ref:`api-prefs-set`), and there is no default value for this preference, ``undefined`` is returned.

.. _api-prefs-set:

``set``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.set(name, value, success, error)

    :param string name: the name of the preference you want to save
    :param value: the value to save
    :param function success: callback to be invoked when no errors occurs
    :param function error: callback to be invoked when an error occurs

The preference value given here will override a default value (if one was given).

``clear``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.clear(name, callback, error)

    :param string name: the name of the preference to un-set
    :param function callback: a callback to be invoked (with no arguments) when the operation is complete
    :param function error: callback to be invoked when an error occurs

Un-sets the given preference name, so that future calls to :ref:`api-prefs-set` will return ``undefined`` (or the default preference value, if given).

``clearAll``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.clearAll(callback, error)

    :param function callback: a callback to be invoked (with no arguments) when the operation is complete
    :param function error: callback to be invoked when an error occurs

Un-sets all preference names, so that calls to :ref:`api-prefs-set` will return ``undefined`` (or the default value for a preference, if given).

``keys``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: prefs.keys(callback, error)

    :param function callback: invoked with an array of the set key names as its only argument
    :param function error: callback to be invoked when an error occurs

Find which preferences have been set.
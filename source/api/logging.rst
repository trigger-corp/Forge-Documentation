.. _logging:

Logging: ``forge.logging``
================================================================================

Allows you to log a message, and optionally an exception, to the console service provided by the underlying platform.

The ``logging.level`` configuration directive controls the verbosity of the logging system.
It should be set to one of ``DEBUG``, ``INFO``, ``WARNING``, ``ERROR`` or ``CRITICAL``.
A setting of ``DEBUG`` means that all messages will be logged, whereas a setting of ``CRITICAL`` means that only messages of level ``CRITICAL`` will be logged.

.. note:: logging currently doesn't work with the iOS emulator. We are fixing this as a high priority.

``log``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

.. js:function:: logging.log(message[, exception][, level])

    :param message: a string to log on the browser console
    :param exception: a JavaScript Error instance: details from the exception will be appended to your log message
    :param level: importance of this message: one of ``forge.logging.DEBUG``, ``forge.logging.INFO``, ``forge.logging.WARNING``, ``forge.logging.ERROR`` or ``forge.logging.CRITICAL``

.. js:function:: logging.debug(message[, exception])

    Shorthand for ``forge.logging.log(message[, exception], forge.logging.DEBUG)``

.. js:function:: logging.info(message[, exception])

    Shorthand for ``forge.logging.log(message[, exception], forge.logging.INFO)``

.. js:function:: logging.warning(message[, exception])

    Shorthand for ``forge.logging.log(message[, exception], forge.logging.WARNING)``

.. js:function:: logging.error(message[, exception])

    Shorthand for ``forge.logging.log(message[, exception], forge.logging.ERROR)``

.. js:function:: logging.critical(message[, exception])

    Shorthand for ``forge.logging.log(message[, exception], forge.logging.CRITICAL)``
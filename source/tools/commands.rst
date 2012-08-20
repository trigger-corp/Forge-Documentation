
.. _command-line-notes:

Command-line
===========================

There are four main commands when using forge:

* ``forge create``
* ``forge build``
* ``forge run``
* ``forge package``

There are also some additional commands which may be used:

* ``forge check``: Perform some sanity checks on the app, including parsing the Javascript to check for syntax errors.
* ``forge migrate``: Migrate to the next version of Forge, you will be prompted to run this when it is available.

Run any command with the ``--help`` argument to see more information about the particular command.

.. note:: All commands can be run with the ``--verbose`` parameter, to enable the display of more output.

.. _command-line-notes-arguments:

Location of ``forge`` executable
--------------------------------

To run forge commands use the forge executable in your Toolkit installation: 

Windows
~~~~~~~~
.. parsed-literal::

	C:\\> "C:\\Users\\<Your Username>\\AppData\\Local\\Trigger Toolkit\\forge.exe"

Mac users
~~~~~~~~~~
.. parsed-literal::

	$ $HOME/Library/Trigger\\ Toolkit/forge

Linux users
~~~~~~~~~~~~~
.. parsed-literal::

	$ ~/TriggerToolkit/forge

Command-line parameters
------------------------------------------
Parameters to the ``forge`` commands can be given as command-line options, or :ref:`stored in a file <parameters-in-a-file>`.

Command-line options are dot-separated names, like ``--android.sdk /path/to/android-sdk``.

A complete list of command-line options, is given in :ref:`command_line_notes_available_params`.

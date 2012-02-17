.. _command-line-notes:

Command-line Notes
===============================================================================

The ``wm-create``, ``wm-dev-build``, ``wm-prod-build`` and ``wm-run`` commands are now deprecated, in favour of their ``forge`` equivalents:

* ``forge create``
* ``forge build``
* ``forge run``
* ``forge package``

Run any command with the ``--help`` argument to see more information about the particular command.

.. note:: All command line commands can be run with the ``--verbose`` parameter, to enable the display of more output.

Storing parameters to Forge commands in a file
----------------------------------------------

As an alternative to passing parameters to the various ``forge`` commands, it is possible to store these values in a file called ``local_config.json``. This is convenient for reuse of e.g. Keystores/Provisioning Profiles during ``forge package``.

The file must be located along side the ``src/`` directory, an example of using it is: ::

    my-app/
        development/
        src/
        local_config.json

The following shows example content of local_config.json:

.. parsed-literal::
    {
        "provisioning_profile": "/home/trigger/embedded.profile",
        "certificate_to_sign_with": "iPhone Developer",

        "sdk": "/opt/android-sdk-x86/",
        "keystore": "/home/trigger/release.keystore",
        "keyalias": "trigger",
    }

Relation between cmdline and config file

====================== ======================== =================================================================
Commandline Switch     Config Option            Meaning
====================== ======================== =================================================================
--provisioning-profile provisioning_profile     Provisioning Profile to embed into your iOS app           
--certificate          certificate_to_sign_with Name of certificate to sign iOS app with

--sdk                  sdk                      Location of Android SDK
--keystore             keystore                 Location of Java Keystore containing key for signing Android apps
--keyalias             keyalias                 Name of key in the given keystore to use to sign Android apps

====================== ======================== =================================================================

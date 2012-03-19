.. _command-line-notes:

Command-line Notes
===============================================================================

There are four main commands when using forge:

* ``forge create``
* ``forge build``
* ``forge run``
* ``forge package``

Run any command with the ``--help`` argument to see more information about the particular command.

.. note:: All commands can be run with the ``--verbose`` parameter, to enable the display of more output.

.. _command-line-notes-arguments:

Command-line parameters
------------------------------------------
Parameters to the ``forge`` commands can be given as command-line options, or :ref:`stored in a file <parameters-in-a-file>`.

Command-line options are dot-separated names, like ``--android.sdk /path/to/android-sdk``.

A complete list of command-line options, is given in :ref:`command_line_notes_available_params`.

.. _parameters-in-a-file:

Storing parameters to Forge commands in a file
----------------------------------------------

As an alternative to passing parameters to the various ``forge`` commands, it is possible to store these values in a file called ``local_config.json``.
This is convenient for reuse of e.g. Keystores and Provisioning Profiles during ``forge package``.

The file must be located along side the ``src/`` directory, for example::

    my-app/
        development/
        src/
        local_config.json

Format of ``local_config.json``
--------------------------------------------------------------------------------
``local_config.json`` is a JSON file which specifies various runtime parameters of the ``forge`` commands.

There is a *general* section, for parameters which are not linked to any particular target, and then per-target sections: *ios*, *android* and so on:

.. parsed-literal::
  {
    ":ref:`general <local_conf-general>`": {
    },
    ":ref:`ios <local_conf-ios>`": {
      "device": "simulator",
      "profiles": {
        "DEFAULT": {
          "provisioning_profile": "/home/trigger/development.mobileprovision"
        },
        "release": {
          "provisioning_profile": "/home/trigger/release.mobileprovision",
          "developer_certificate": "iPhone Developer: James Brady (5W89HYT9F3)"
        }
      }
    },
    ":ref:`android <local_conf-android>`": {
      "sdk": "/opt/local/android-sdk",
      "profiles": {
        "DEFAULT": {
          "keystore": "/home/trigger/development.keystore",
          "keyalias": "trigger"
        },
        "release": {
          "keystore": "/home/trigger/release.keystore",
          "keyalias": "trigger"
        }
      }
    }
  }

A note on file paths
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You can specify files using a path relative to the current directory, or you can use an absolute path.

On Windows, you will need to escape the backslashes in paths for your configuration file, e.g.::

    {
        "andoid": {
            "sdk": "C:\\Users\\Tim Monks\\android-sdk-windows"
        },
        "profiles": {
            "DEFAULT": {
                "keystore": "..\\default.keystore"
            }
        }
    }

.. _local_conf-profiles:

Profiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the target-specific sections (e.g. *ios*, *android*), you can use *profiles*.

Profiles allow for quick switching between configuration settings at different phases of your development.

For example, you need to use different credentials to sign iOS apps when creating builds for testing and builds for deployment to the App Store.

By creating a different profile in this section, you can quickly change between collections of configuration settings by naming a profile with the ``--profile`` command-line argument.

If no ``--profile`` argument is given, Forge attempts to use a profile called ``DEFAULT`` - it's case sensitive, so you can create and use a profile called ``default`` if you wish, for example.

.. important:: When supplying command-line overrides to profile settings, they take a form like ``--ios.profile.name value``, where ``name`` is the setting name to be overidden, and ``value`` is the setting value.

.. _command_line_notes_available_params:

Available Forge Parameters
------------------------------------------

.. _local_conf-general:

general
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
General parameters are configuration settings not related to any particular target.

There are no settings currently used in this section.

.. _local_conf-ios:

ios
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This section contains settings pertaining to building and running Forge apps for iOS.

The device to use when running iOS apps is not profile-specific:

======================== =================================== ===============================================================
Config Option            Command-line Option                 Meaning
======================== =================================== ===============================================================
device                   --ios.device                        Either ``simulator``, ``device`` or a specific device ID
======================== =================================== ===============================================================

All other settings should be placed inside a :ref:`profile <local_conf-profiles>`: available settings are shown below:

======================== =================================== ===============================================
Profile Config Option    Command-line Option                 Meaning
======================== =================================== ===============================================
provisioning_profile     --ios.profile.provisioning_profile  Provisioning Profile to embed into your iOS app
developer_certificate    --ios.profile.developer_certificate Name of certificate to sign iOS app with
======================== =================================== ===============================================

.. _local_conf-android:

android
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use this section for settings relating to building and running Forge apps for Android.

The location of the Android SDK is not profile-specific:

======================== =================================== ===============================================================
Config Option            Command-line Option                 Meaning
======================== =================================== ===============================================================
sdk                      --android.sdk                       Path to the Android SDK on your machine.
device                   --android.device                    Device identifier to run your app on, e.g. ``323406C1AD9090EC``
purge                    --android.purge                     Completely reset all state of the app before running.
======================== =================================== ===============================================================

The other settings should be in a :ref:`profile <local_conf-profiles>`:

======================== =================================== ===============================================
Profile Config Option    Command-line Option                 Meaning
======================== =================================== ===============================================
keystore                 --android.profile.keystore          Path to your :ref:`keystore <releasing-keystore>`
keyalias                 --android.profile.keyalias          Alias given to your key in the keystore
storepass                --android.profile.storepass         Password for your keystore
keypass                  --android.profile.keypass           Password for your key
======================== =================================== ===============================================

We recommend using the command-line switches for ``storepass`` and ``keypass``, rather than placing them in a configuration file, for security reasons.

Working behind a Proxy
----------------------
If you're having trouble running the tools behind a proxy server, you can
modify ``forge_build.json`` in the directory where you installed the forge
tools to look like:

.. parsed-literal::
  {
    "main": {
        "server": "https://trigger.io/api/",
        "proxies": {
            "https": "my.proxy.com:8080"
        }
    }
  }

.. note:: Make sure to specify the proxy for **https** as all traffic to our services is over https.

Excluding files and folders from your builds
--------------------------------------------
To exclude files and folders in ``src`` from being included in the output of
``forge build``, you can write a set of exclusion rules in
``src/.forgeignore``. The following is an example ``.forgeignore`` file::

    ignoreme.txt
    *.swp
    ./tests/
    .git/
    ./identity.json

There are two types of exclusion rules: rules that check the *filename* of each
file and rules that check the *path* of each file (relative to the ``src``
directory).

*Excluding files based on their name*:
    Any rule without a / symbol in it is a filename rule. If you want to
    exclude any files called ``ignoreme.txt``, the correct pattern to use is
    just ``ignoreme.txt`` as shown above.

*Ignoring files with a specific extension*:
    Filename rules support glob syntax, so you can have rules that only
    consider part of the name. For example, ``*.swp`` will ignore
    ``index.html.swp`` and ``main.js.swp``.

*Ignoring all folders with a certain name (but not files)*:
    To exclude folders that match a rule but not files that match the rule,
    just add a trailing / symbol. E.g. ``.git/`` will exclude any folders
    called ``.git`` but include individual files with the same name.

*Ignoring a file at a specific path*:
    If you want to exclude a file at a particular location in your code, just
    specify the path to it. E.g. ``./identity.json`` will exclude
    ``identity.json`` at the top level of your ``src``, but any other files
    with that name will be included.

    Paths support globs too, so e.g. ``./temp/*.js`` will ignore all files
    matching ``*.js`` inside the temp folder.

.. note:: Windows users should make sure to always use / symbols as the folder separator (*forward slashes*) in your forgeignore file, these will ensure the exclusion rules work across different platforms

.. _native_plugins_common_problems:

Common problems
===============

This page details some of the common problems when developing plugins. If you can't find information on the problem you are having then you can email support@trigger.io or check http://stackoverflow.com/questions/tagged/trigger.io.

Toolkit error messages
----------------------

As plugins have a greater affect on the build process it is far easier for a
plugin to cause issues when trying to build an app using it, to limit this the
Toolkit will try to detect common problems while you develop your plugin. This
page contains some more detailed information about the various errors that can
appear while developing, and how you can fix them.

iOS/Android inspector not found
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is shown when your plugin contains an Android or iOS folder but no matching
inspector project is found.

iOS/Android inspector out of date
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This message is shown when your current inspector project was not created with
the files included in your plugins folder and with the current plugins platform
version. This generally indicates you should update your inspector project
before continuing development.

The directory 'x' was expected to be a file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This error is shown if a directory is found in a location that a file was
expected, for example if a plugins jar file was actually an extracted folder
rather than a compressed file.

The file 'x' was expected to be a directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Similarly this error is shown if a file is found in a location that was expected
to be a directory. An example of this would be if an iOS bundle was a file, iOS
bundles are actually a special type of directory that appears as a single file
in Finder.

The path 'x' is required and was not found
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This error means a file that is required based on the current structure of your
plugin was not found. The most common example of this is if an ``android``
folder is found within your plugin then a ``plugin.jar`` file must be included
within that folder.

The path 'x' was found but not expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This warning means a file or directory was found with a path that was not
expected, this generally won't cause a problem in itself, but this file will not
be used when including the plugin in a Forge build, and could mean it is named
incorrectly or placed in the wrong location.

File 'android/plugin.jar' is not a valid jar file containing a Forge Android plugin with name 'x'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Toolkit checks the jar file for your plugin contains a class which looks
like it belongs to your plugin, if it can't find it then something is probably
wrong with the structure of your code or with the way you created you jar file.
Check your plugin is named correctly and you include a API.java for that module
name in your jar, if you still see problems then get in touch so we can look
into it.

File 'ios/plugin.a' is not a valid static library file containing a Forge iOS plugin with name 'x'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Toolkit checks your built iOS plugin contains classes that look like they
belong to your plugin, if it can't find them then something is probably wrong
with the file you've built. Read through the docs and rebuild your plugin, if
you can't solve the problem get in touch and we'll be able to help you out.

Validation for 'x' failed: ...
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If your error message isn't explictly listed above but starts with this text it
means the given file failed some kind of pre-upload validation we perform, often
a more descriptive error message will be given. Check the file follows this
documentation and if you still can't resolve the issue get in touch.

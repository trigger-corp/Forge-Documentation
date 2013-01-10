.. _tools-toolkit:

The Trigger.io Toolkit
==============================================================================

The Trigger.io Toolkit is a graphical interface to start / stop builds, package your app, push :ref:`Reload <modules-reload>` updates to your users and create :ref:`native plugins <native_plugins>`.

It offers more functionality than the :ref:`command-line tools <command-line-notes>` and is the preferred user interface for new and existing Trigger.io users.

Installing the Trigger.io Toolkit
------------------------------------------------------------------------------
You can download the Toolkit installer from https://trigger.io/forge/toolkit/.

Follow the OS-specific instructions on the download page to install and start the Toolkit.

Common tasks in the Trigger.io Toolkit
------------------------------------------------------------------------------

Creating a new project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Open the toolkit and click the "Create a new project" button.

A page on our website will be opened so that you can enter the new project name and select a project plan.

.. image:: /_static/images/toolkit__create_new_project.png
	:width: 500px
	:target: ../_static/images/toolkit__create_new_project.png

Creating a new app
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Enter into a project by clicking on its name, then click the "Create new app" button (shown in pink).

If one of your colleagues has sent you the source code for an existing app, chose "Import existing app" (shown in blue) and navigate to where the source is on your computer.

.. image:: /_static/images/toolkit__create_new_app.png
	:width: 500px
	:target: ../_static/images/toolkit__create_new_app.png

Creating a new plugin
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Inside a project, click the "Create new plugin" button.

This option will only be available if plugins are enabled for this project - contact support@trigger.io for more information.

.. image:: /_static/images/toolkit__create_new_plugin.png
	:width: 500px
	:target: ../_static/images/toolkit__create_new_plugin.png

Changing the configuration for an app
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Enter into an app by clicking on its name, then click on the "App config" tab.

See :ref:`config` for more information about how to use this interface.

.. image:: /_static/images/toolkit__app_config.png
	:width: 500px
	:target: ../_static/images/toolkit__app_config.png

Running an app on an iOS device
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
You may want to first update your Toolkit configuration to run the app on the right device or emulator.

Enter the Local config tab (marked in pink) then update the three settings concerning running iOS apps (marked in blue).

See :ref:`parameters-in-a-file` for more information about how to use this interface.

.. image:: /_static/images/toolkit__ios_local_config.png
	:width: 500px
	:target: ../_static/images/toolkit__ios_local_config.png

Then, click on "iOS" in the "Run" section to start the app running.

.. image:: /_static/images/toolkit__run_ios.png
	:width: 500px
	:target: ../_static/images/toolkit__run_ios.png

Running an app on Android
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In the same way as iOS, extra configuration parameters are available for Android in the Local config tab, but you normally don't need to update these.

Just click on "Android" in the "Run" section to start the app running on a device (if one is attached) or to start the emulator.

.. image:: /_static/images/toolkit__run_android.png
	:width: 500px
	:target: ../_static/images/toolkit__run_android.png

.. _reload:

Using Trigger.io Reload
===========================

Trigger.io Reload allows you to update the HTML, CSS and JavaScript in your app for your users without you needing to push an Appt Store update or your users needing to re-install the app.

Read about the :ref:`Reload module <modules-reload>` to enable it and :ref:`learn about the concepts <reload_concepts>`. Once you have the module enabled you can push updates to your existing users through the Toolkit UI:


How to reload an update with the Toolkit UI
---------------------------------------------

Use the Reload tab in the Toolkit to manage your streams and push updates

.. image:: /_static/images/toolkit-reload.png

In this tab, you can manage your streams of users - this allows you to push different code to different users for A/B testing. By default there is a single stream which enables you to push to all users without any extra configuration.

You can also see your configurations here - how many unique users we have detected that are using your app built against which minor version of the Forge platform.

Once you have built and tested new code that you wish to deploy, you can click the 'Push to stream' link from this view in order to push the update.

Using reload from the command line
----------------------------------

Some of the functionality of reload can be accessed via the command line, which allows automation of certain tasks, such as pushing an update. The commands available are:

* ``forge reload list``: This will list all available streams for your app
* ``forge reload create <streamname>``: This will create a stream called ``<streamname>`` which can then be pushed to.
* ``forge reload push <streamname>``: This will push the last build to ``<streamname>``, it is likely you will want to run ``forge build reload`` directly before this command in order to build your current ``src`` folder.

Gotchas
----------------------------------

Currently, pushing a Reload update will cause iOS devices to copy files out of the installed app bundle into a secondary area. This is due to sandboxing rules which prevent us directly accessing files in your installed app after a Reload has been completed. In order to avoid your app taking too much storage space on the device, it's recommended you distribute larger files using something like :ref:`forge.file.saveURL <modules-file>`, rather than including them in the app bundle.

We are actively looking for a way to avoid this limitation.
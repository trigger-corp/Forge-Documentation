.. _reload:

Using Trigger.io Reload
===========================

Trigger.io Reload allows you to update the HTML, CSS and JavaScript in your app for your users without you needing to push an App Store update or your users needing to re-install the app.

You can push your app content updates via Trigger.io's servers for app sizes up to 250Mb. For larger content, or if you want to host content that is to be re-used in your web app or other apps, then you can :ref:`Reload with a 3rd party CDN like Rackspace Cloud Files <reload-cdn>`.

Read about the :ref:`Reload module <modules-reload>` to enable it and :ref:`learn about the concepts <reload_concepts>`. 

Once you have the module enabled you can push updates to your existing users through the Toolkit UI, command-line tools or :ref:`standalone build API <standalone-reload>`.



How to reload an update with the Toolkit UI
---------------------------------------------

Use the Reload tab in the Toolkit to manage your streams and push updates

.. image:: /_static/images/toolkit-reload.png

In this tab, you can manage your streams of users - this allows you to push different code to different users for A/B testing. By default there is a single stream which enables you to push to all users without any extra configuration.

You can also see your configurations here - how many unique users we have detected that are using your app built against which minor version of the Forge platform.

Once you have built and tested new code that you wish to deploy, you can click the 'Push to stream' link from this view in order to push the update.


.. _reload-command-line:

Using reload from the command line
----------------------------------

Some of the functionality of reload can be accessed via the command line, which allows automation of certain tasks, such as pushing an update. The commands available are:

* ``forge reload list``: This will list all available streams for your app
* ``forge reload create <streamname>``: This will create a stream called ``<streamname>`` which can then be pushed to.
* ``forge reload push <streamname>``: This will push the last build to ``<streamname>``, it is likely you will want to run ``forge build reload`` directly before this command in order to build your current ``src`` folder.

.. _reload-cdn:

Reloading app content from Rackspace Cloud Files or other CDN
-----------------------------------------------------------------------

Concepts
~~~~~~~~~

If you are building a content-heavy app including large images or videos it is recommended that you host the app content and Reload it from a CDN like `Rackspace Cloud Files <http://www.rackspace.com/cloud/files/>`_. 

You must use a CDN with Reload if your app size is greater than 250Mb.

CDNs are optimized for download performance according to your users' locations. Hosting your app content on a CDN with Reload enables you to push large content files down to your app in the background, and link to the same content from your web app or other mobile apps.

Using Reload with a CDN enables you to overcome the challenges of large content in mobile apps. Your app must:

* Be small to allow for fast download onto the device
* Have content local to the app for fast performance and a great offline experience
* Be able to access new content to keep the user engaged

With Reload and a CDN you can have a small app hosted on the App Store or Google Play which downloads large content in the background. 

The process
~~~~~~~~~~~~

When you push a Reload via a CDN the end-user experience is the same and you are able to use the same :ref:`Reload APIs <reload-api>` in your app code.

The process for pushing the Reload has some extra steps. You can see these steps in action with our `screencast tutorial demonstrating Reload integrated with Rackspace Cloud Files <https://vimeo.com/62121831>`_.

The process is:

#. :ref:`Enable Reloads from a CDN in your Local Config <local_conf-general>`
#. `Create a Reload manifest file <https://github.com/trigger-corp/make_manifest>`_
#. Upload the manifest file and files to be reloaded to your CDN and make them publicly available
#. Push your Reload using the Toolkit UI or :ref:`standalone build API <standalone-reload>`

You can use the :ref:`standalone build API to push a Reload hosted on a CDN <standalone-reload>` in which case you must perform steps 2 and 4 manually at the command-line. You can find detailed instructions for those steps by clicking through the links against them above.

But the simplest way is to use the Toolkit UI which automates steps 1 and 4.

.. _reload-cdn-toolkit:

How to push a Reload hosted on a CDN via the Toolkit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Having :ref:`enabled Reloads from a CDN in your Local Config <local_conf-general>`:

* Go to the Reload tab in your Toolkit, select the config and stream you would like to push to
* Click 'Push to stream' and you will be prompted to provide a CDN URL and Manifest URL


.. image:: /_static/images/toolkit-cdn-reload.png


* Once you've entered the CDN URL, you can use 'Generate Manifest' button to automatically create the manifest files and app files in a temporary directory. You should upload all of those files to your CDN.
* Clicking 'Generate Manifest' also populates the Manifest URL field. You must make sure that the url you specified in 'CDN URL' is in fact the root url where your manifest and other files will be hosted.
* Finally, click the 'Push' button to start the Reload

Gotchas
----------------------------------

Currently, pushing a Reload update will cause iOS devices to copy files out of the installed app bundle into a secondary area. This is due to sandboxing rules which prevent us directly accessing files in your installed app after a Reload has been completed. In order to avoid your app taking too much storage space on the device, it's recommended you distribute larger files using something like :ref:`forge.file.saveURL <modules-file>`, rather than including them in the app bundle.

We are actively looking for a way to avoid this limitation.
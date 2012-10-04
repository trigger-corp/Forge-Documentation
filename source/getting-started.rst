.. _forge-index:

Getting Started with Forge
==================================

To use Forge, you will first need to install the toolkit from: https://trigger.io/forge/toolkit

After completing the install process, start the toolkit and you will be prompted to create an account. You can use the toolkit UI to build and test your apps or you can use the command-line tools that are bundled with the toolkit.

Read on to get started with the toolkit or learn about :ref:`command_line_setup`

Getting started with the toolkit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Read the instructions on the `toolkit download page <https://trigger.io/forge/toolkit>`_ to learn how to install and start the toolkit on your platform.

After signing up or logging in, you will see your Your Apps. You can always return to this screen by clicking "Manage Apps" in the header. At first no apps will be listed here.

.. image:: /_static/images/your-apps.png

Creating your first app
-----------------------

Click the "Create" link at the bottom-left to create a new app. You will be prompted for an name and location and then you will be returned to Your Apps where you will now see the new app listed.

Congratulations, you've created your first app and are ready to build and test it.

Working with an existing app
-----------------------------------------------

If you have an existing app, for example you may have cloned it from an existing Github repos or created it with the command-line tools, then you will need to import it.

Simply click the "Import" link at the bottom-right of Your Apps. You will be prompted for the location and then returned to Your Apps where you will now see the app listed ready to be built and tested.

What next?
-----------------------------------------------
By now, you have a development environment set up.

From here, you could take a look at:

- :ref:`mobile-index`
- :ref:`web-index`
- :ref:`chrome-index`
- :ref:`tutorials-weather-tutorial-index`

.. _command_line_setup:

Getting started with the command-line tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To run forge commands use the forge executable in your Toolkit installation. 

.. note:: It is recommended that you add the directory that the forge executable is in to your path, otherwise you will have to use the full path to the forge executable each time you want to run any ``forge`` command.

Windows
-------------
.. parsed-literal::

	C:\\> "C:\\Users\\<Your Username>\\AppData\\Local\\Trigger Toolkit\\forge.exe" create

Mac users
-------------------
.. parsed-literal::

	$ $HOME/Library/Trigger\\ Toolkit/forge create

Linux users
-------------------
.. parsed-literal::

	$ ~/TriggerToolkit/forge create

.. _forge-create-app:

Creating your first app
-----------------------

.. note:: If you have an existing app you'd like to work with, see :ref:`forge-existing-app`.

To keep each of your apps separate, we expect that you will want to work on them in different directories. In the terminal, we'll create a new directory and move into it::

    mkdir "../demo-app"
    cd "../demo-app"

Now, we'll create our app, with the ``forge create`` command::

  $ forge create
  [   INFO] Forge tools running at version 1
  Enter app name: 

At this point a descriptive name for your new app: if you're planning on following along with our tutorial, "Weather Demo" would be a reasonable choice.

If this is the first time you're running this command, you will be prompted to log in with the email address and password that you signed up with at the Forge website::

  $ forge create 
  [   INFO] Forge tools running at version 2.3.1
  Enter app name: Weather Demo
  Your email address: james@trigger.io
  Password: 
  [   INFO] authenticating as "james@trigger.io"
  [   INFO] authentication successful
  [   INFO] fetching initial project template

At this point, you're ready to edit your app and start running builds!

If you're starting your app in Chrome, take a look at our :ref:`Chrome tutorial <chrome-index>`. Or, you can also follow the same tutorial on :ref:`Mobile <mobile-index>`.

.. _forge-existing-app:

Working with an existing app
-----------------------------------------------
If you are already working with an app on your machine, simply change directory to where the app is::

    cd "../my-existing-app"

In that directory, you should have a ``src`` directory, containing the code for your app. For further documentation, follow our :ref:`Chrome tutorial <chrome-index>`, :ref:`Mobile tutorial <mobile-index>` or see our :ref:`modules`.

What next?
-----------------------------------------------
By now, you have a development environment set up.

From here, you could take a look at:

- :ref:`mobile-index`
- :ref:`web-index`
- :ref:`chrome-index`
- :ref:`tutorials-weather-tutorial-index`

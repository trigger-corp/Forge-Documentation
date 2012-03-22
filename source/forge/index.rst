.. This folder will document how to get started using the forge website, from creating an account through to having created your first app.

.. _forge-index:

Getting Started with Forge
==================================

To use Forge, you will first need to sign up for the service at https://trigger.io/forge/

After completing the registration process, you will be prompted to download the Forge development environment. This is distributed as a zip file and can be extracted anywhere you please.

If you don't have Python installed you will need to install a recent `2.x version <https://trigger.io/forge/requirements/>`_ first (see `here <http://www.python.org/getit/>`_ for other releases and options).

Windows users
-------------
* run ``go.bat`` by double-clicking on it

Mac and Linux users
-------------------
* open a terminal
* change directory to wherever you extracted the zip file
* run ``source go.sh``

Now go on to :ref:`creating your first app <forge-create-app>`.

.. _forge-create-app:

Creating your first app
-----------------------

.. note:: If you have an existing app you'd like to work with, see :ref:`forge-existing-app`.

At this point, you should have a command terminal open that looks something like::

  (forge-environment)

To keep each of your apps separate, we expect that you will want to work on them in different directories. In the terminal, we'll create a new directory and move into it::

    mkdir "../demo-app"
    cd "../demo-app"

Now, we'll create our app, with the ``forge create`` command::

  (forge-environment) forge create
  [   INFO] Forge tools running at version 1
  Enter app name: 

At this point a descriptive name for your new app: if you're planning on following along with our tutorial, "Weather Demo" would be a reasonable choice.

If this is the first time you're running this command, you will be prompted to log in with the email address and password that you signed up with at the Forge website::

  (forge-environment) forge create 
  [   INFO] Forge tools running at version 2.3.1
  Enter app name: Weather Demo
  Your email address: james@trigger.io
  Password: 
  [   INFO] authenticating as "james@trigger.io"
  [   INFO] authentication successful
  [   INFO] fetching initial project template
  (forge-environment)

At this point, you're ready to edit your app and start running builds!

If you're starting your app in Chrome, take a look at our :ref:`Chrome tutorial <chrome-index>`. Or, you can also follow the same tutorial on :ref:`Mobile <mobile-index>`.

.. _forge-existing-app:

Working with an existing app
-----------------------------------------------
If you are already working with an app on your machine, after activating the ``forge-environment``, simply change directory to where the app is::

    cd "../my-existing-app"

In that directory, you should have a ``src`` directory, containing the code for your app. For further documentation, follow our :ref:`Chrome tutorial <chrome-index>`, :ref:`Mobile tutorial <mobile-index>` or see our :ref:`api`.

.. _web-index:

Forge and the Web
=================================================

In addition to creating native mobile and browser apps, Forge apps can be deployed to the open web
for access by mobile and desktop browsers. This means you don't need to decide between focusing on
native apps or mobile websites. Both can be created from the same HTML5 code base using the Forge
framework.

Forge web apps are built upon node.js for optimum portability. The Forge build tools handle everything
required to build and deploy your code.

Testing your web app
--------------------
First off you'll need a Forge application. If you're not yet set up in Forge, try our
:ref:`Getting Started Guide <forge-index>` then our :ref:`Chrome <chrome-index>` or
:ref:`Android <android-index>` tutorials to learn the basics - or you could download one of our
`demo apps <http://docs.trigger.io/en/v1.2/android/getting-started.html#building-the-code>`_
from GitHub.

Running ``forge build`` from your app's root directory creates the code for your web application alongside
your mobile apps in just a few seconds (see
`Building the Code <http://docs.trigger.io/en/v1.2/android/getting-started.html#building-the-code>`_
if this is your first time building a Forge app).

You can view the web app in your desktop browser by running ``forge run web``. This will open a new tab
in your browser displaying your app.

.. note:: Even if you don't plan to deploy to the web, this is a great place to inspect the DOM and debug your
   Javascript using the Chrome Developer Tools or the Firebug plugin for Firefox

Deploying your web app on Heroku
--------------------------------
Your generated web app can be deployed to any node.js platform. To make deployment really easy, we've
added an option to deploy the app directly to `Heroku <http://www.heroku.com>`_ with a single command line command.

The steps for doing this are:

* Set up a Heroku account if you haven't already. You can do this by following the steps in their
  `tutorial <http://devcenter.heroku.com/articles/quickstart>`_. No need to deploy an application at this stage.
* Return to your app directory and run ``forge build`` to ensure your latest changes are included in the
  generated web app.
* Run ``forge package web``. If it is the first time you've done this for an application, the command line tool
  will ask if you want to create a new Heroku app or deploy to an existing Heroku app in your account.

That's it! Your app will be live on Heroku (the web address will be given at the command line output).
You can link this to your domain name by following instructions on the Heroku site.

Repeat steps 2 and 3 each time you want to update the deployed app.

Deploying your web app to any node.js platform
----------------------------------------------
The web application created by ``forge build`` lives in <your-app-folder>/release/web/heroku. You can take
the code from here and deploy to your favorite node.js platform like any other node.js web app.

Best practices
--------------
* Use ``forge.is.web()`` in the Forge Javascript framework to detect whether your app is running in a
  mobile browser and make any functionality or layout changes required. For example, a photo sharing app may
  hide native camera functionality in a web browser but show it in a mobile app.

* If you intend your output to be viewed in a desktop browser, be mindful of how it will look at this much
  larger screen size and design your CSS accordingly.

* Test often with ``forge run web``.

What do you think?
------------------
If you have any outstanding questions or feedback we'd love to hear from you at support@trigger.io.
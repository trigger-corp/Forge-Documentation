.. _facenote-tutorial-1:

Tutorial Part 1
==============================================================================

In this tutorial, we will use the Forge platform to create a browser extension which lets users attach text notes to profiles on Facebook.

As this particular app is based around modifying the contents of web pages on-the-fly, it is not applicable to mobile app development: see :ref:`our weather app tutorial <weather-tutorial-1>` for how to get started with a mobile app.

.. contents::
   :backlinks: none

Goal
----
By the end of this part of the tutorial, you will have a development environment set up to embed your JavaScript code into Facebook pages.

What you'll need
----------------
* an internet connection
* `Google Chrome <http://www.google.com/chrome/>`_: version 5 or higher
* a working knowledge of HTML, CSS and JavaScript debugging tools like the `Chrome Developer Tools <http://code.google.com/chrome/devtools/docs/overview.html>`_
* about an hour of your time

Preparation
-----------
Firstly, follow the :ref:`forge-index` instructions. This will leave you with a browser extension to be customised to your particular needs.

This will leave you with a ``src`` directory (where all your code will be placed), containing a ``config.json`` file.

Update the extension name and description
-----------------------------------------
A cosmetic change, but an important one, is setting the name and description for your extension. Depending on the browser, this may appear during the install process and on the list of installed extensions.

Open ``config.json`` from the ``src`` folder created above, and change the name and description::

  "name": "Facebook note demo",
  "description": "A demo application: lets users attach notes to Facebook profiles",

Building the app
---------------------------------
To build the extension, bring up your terminal, and enter the ``forge build`` command::

    $ forge build
    [   INFO] Forge tools running at version 1.0.1
    [   INFO] configuration has changed: creating new templates
    [   INFO] starting new build
    [   INFO] build 11 started...
    [   INFO] build completed successfully
    [   INFO] current configuration hash is 564c9ef0ede72b76ce06b823047f075a
    [   INFO] fetching new Forge templates
    [   INFO] fetching unpackaged artefacts for build 532 into ".template"
    [WARNING] creating output directory ".template"
    [   INFO] Development build created. Use forge run to run your app.

Underneath the ``development/chrome`` directory, you now have a development Chrome extension which can be installed from the ``chrome://extensions`` screen. Following these instructions, `create and load an extension <http://code.google.com/chrome/extensions/getstarted.html>`.

.. warning:: Whenever you make changes to files in the ``src`` directory, you will need to rebuild the app with ``forge build``, then reload the extension by going to ``chrome://extensions`` and clicking on *Reload* in the relevant section.

Activating on the right pages
----------------------------------
This particular browser extension should only be activated on Facebook pages.

To set this up, we need to change the ``patterns`` array in ``config.json``. Change this::

    "patterns": ["http://*/*"],
    
    
To this::

  "patterns": ["http://www.facebook.com/*", "https://www.facebook.com/*"],

The ``"http://www.facebook.com/*"`` value is a `match pattern <http://code.google.com/chrome/extensions/match_patterns.html>`_ dictating which URLs the extension should activate on.

Customise the JavaScript
------------------------
**Goal: run some JavaScript when Facebook pages load**

Currently, the extension doesn't run any JavaScript when your extension activates. In this section, we'll create a new JavaScript file and configure the extension to load it on the right pages.

Firstly, in the ``src`` directory, create a file called ``fb-note-demo.js``. Open ``fb-note-demo.js`` in your preferred text editor, and add this code::

    alert("Facebook demo extension loaded");

Include your JavaScript in your extension
-----------------------------------------

The JavaScripts we embed are defined in ``src/config.json``, in the ``scripts`` array. Change this::

  "scripts": []

to this::

  "scripts": [
    "/fb-note-demo.js"
  ]

Now, rebuild your extension with ``forge build`` and reload it in Chrome. When you go to a Facebook page, you should see your own alert popup.

Reference extension
-------------------
`fb-part-1.zip <../_static/facenote/part-1.zip>`_ contains the code you should have at this point. Feel free to check your code against it, or use it to resume the tutorial from this point.

It's not working!
-----------------
Things to check:

* have you updated ``src/config.json`` to point at the modified local copy of ``fb-note-demo.js``?
* have you reloaded your extension?
* on Facebook, use `Chrome's Developer Tools <http://code.google.com/chrome/devtools/docs/overview.html>`_ to see which scripts have been embedded in the page: do you see a HTTP 404 for your JavaScript file?
* on Facebook, use the console in Chrome's Developer Tools to check for JavaScript errors: uncaught exceptions may cause the alert messages not to appear
* clearing your browser cache (at ``chrome://history/#e=1&p=0``) will flush out any old resources
* still not working? Get in touch at support@trigger.io!

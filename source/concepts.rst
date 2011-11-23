.. _extension-concepts:

Concepts
========

**NB** this documentation only concerns browser extensions, not mobile apps.

Extensions built on the WebMynd platform have two main aspects:

#. code to run when the browser is started
#. code to run when a page loads

.. _extension-concept-background:

Code run at startup: "background code"
--------------------------------------
If your extension relies on long-running code which is not attached or associated with any particular web page, you should use background code.
This code is loaded once when the browser is open or extensions is loaded/reloaded. It runs until the browser is closed or the extension is removed.
It is good practice to put page independent logic/functionality in the background.
JavaScript files which are intended to be run in the background should be added to the :ref:`background-files <field-background_files>` array of the configuration file.

.. _extension-concept-content-scripts:

Code run at page load: "content scripts"
-----------------------------------------
If your extension works with the individual web pages a user sees, you should use content scripts. For example, an extension which changes a web page so that any long words are replaced with links to that word in an online dictionary.

.. _extension-concept-popup:

Code run when a button is clicked: "popup code"
-------------------------------------------------
If your extension includes a :ref:`default_popup <field-default_popup>` section in the config, you can include JavaScript in the HTML file which is shown when a user clicks on a toolbar icon.

This JavaScript is executed each time the popup is opened, and is destroyed when the popup is closed; therefore, it is closer conceptually to content scripts than background code.
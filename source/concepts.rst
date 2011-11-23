.. _extension-concepts:

Concepts
========

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

Code run at page load: "content script"
--------------------------------------------------------------------------------------------------
If your extension works with the individual web pages a user sees, you should use content scripts.
For example, an extension which changes a web page so that any long words are replaced with links to that word in an online dictionary.
Content scripts are loaded every time a page is loaded and its url matches the activations :ref:`pattern<field-activations>` specified in the configuration file.
These scripts should be specified inside the :ref:`scripts <field-activations-scripts>` array of the configuration file.
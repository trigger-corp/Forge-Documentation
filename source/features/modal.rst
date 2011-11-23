.. _forge-modal:

Modal views
================================================================================

Modal views are a mobile only feature of Forge.

Modal views allow a second webpage to be loaded "on top" of the main web view in a Forge app. This allows a second page to be displayed without reloading the original, and also provides a dedicated button on the users screen to close the second view when their interaction has ended.

Modal views have two main purposes, the first is to provide quick access to part of your app without breaking the current workflow, and the second is to access an external site to perform a task such as authentication without the chance of the user being "trapped" on the external site if their device has no back button.

Internal pages
~~~~~~~~~~~~~~

A simple use case for modal views is to display an options page at any point when users are interacting with a Forge app. This means an options page can be displayed, interacted with and closed, without the current page losing its state. To achieve this simply create a separate options page and when you want to display it use ``forge.tabs.open('options.html')``.

External authentication
~~~~~~~~~~~~~~~~~~~~~~~

A more advanced use of modal views is to send the user to an external site (potentially your own website), to allow them to authenticate in some way. In this scenario it is possible to close the modal view and redirect the user to a new local page once the authentication process is complete by redirecting the user to a ``forge:///`` url. An example of how this could be used would be:

#. Call ``forge.tabs.open("https://example.com/login/")``
#. The user logs in to your website
#. Assuming the login is successful your website sets a cookie and redirects the user to ``forge:///loggedin.html``
#. The modal view will close automatically, and the original web view will load the local page ``loggedin.html``
#. ``forge.request.ajax()`` requests made by your app will send the cookie your website set, any requests can then be checked against the previous authentication.
.. _forge-modal:

Modal views
================================================================================

:ref:`Modal views<modules-tabs>` are a mobile only feature of Forge.

Modal views allow a second webpage to be loaded "on top" of the main web view in a Forge app. This allows a second page to be displayed without reloading the original, and also provides a dedicated button on the users screen to close the second view when their interaction has ended.

Modal views have two main purposes. The first is to provide quick access to part of your app without breaking the current workflow, and the second is to access an external site to perform a task such as authentication without the chance of the user being "trapped" on the external site if their device has no back button.

Internal pages
~~~~~~~~~~~~~~

A simple use case for modal views is to display an options page at any point when users are interacting with a Forge app. This means an options page can be displayed, interacted with and closed, without the current page losing its state. To achieve this simply create a separate options page and when you want to display it use ``forge.tabs.open('options.html')`` (see :ref:`the API documentation<modules-tabs-open>`).

External authentication
~~~~~~~~~~~~~~~~~~~~~~~

A more advanced use of modal views is to send the user to an external site (potentially your own website), to allow them to authenticate in some way. At this point there are two options, if you control the remote server you can redirect to a ``forge:///`` url, or whether you control the remote server or not you can watch for a url match pattern and close the modal view when it is found.

Remote redirect
---------------

In this scenario it is possible to close the modal view and redirect the user to a new local page once the authentication process is complete by redirecting the user to a ``forge:///`` url. An example of how this could be used would be:

#. Call ``forge.tabs.open("https://example.com/login/")``
#. The user logs in to your website
#. Assuming the login is successful your website sets a cookie and redirects the user to ``forge:///loggedin.html``
#. The modal view will close automatically, and the original web view will load the local page ``loggedin.html``
#. ``forge.request.ajax()`` requests made by your app will send the cookie your website set (any requests can then be checked against the previous authentication)

Match pattern
-------------

To watch for a match pattern use code similar to::

  forge.tabs.openWithOptions({
    url: 'http://my.server.com/login/',
    pattern: 'http://my.server.com/loggedin/*'
  }, function (data) {
    forge.logging.log(data.url);
  });

See :ref:`the openWithOptions API documentation<modules-tabs-openWithOptions>`.

In this example the final url in the modal view will be logged, data could also be extracted from it and used to authenticate the user, such as the query string (used for OAuth 1) or the hash fragment (in OAuth 2).

.. _forge-cache:

Caching files
================================================================================

File caching a mobile only feature of Forge.

File caching allows you to download a remote resource (such as an image), and keep a reference to the local file. These can then be used in the future to display to the user, even if no internet connection is available. Importantly it is possible to save Forge file objects as Forge preferences which will be persisted between app launches.

Example
-------

This is a quick example of how we can store the logo to our site locally without having to include it in our app when we build it. In this example we download the Forge logo from the Trigger.io site: https://trigger.io/forge-static/css/trigger/f/logo-header-small-forge.png.

Downloading and storing file reference
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First we need to be able to cache the file and save the file object to use later.

Example::

  var cacheLogo = function () {
    forge.file.cacheURL("https://trigger.io/forge-static/css/trigger/f/logo-header-small-forge.png", function (file) {
      // File cached save the file object for later
      forge.prefs.set("logo-cache", file, function () {
        // Logo saved
        showCachedLogo(file);
      });
    });
  }

Checking cached file
~~~~~~~~~~~~~~~~~~~~

Cached files may be deleted by the operating system to free up space, you should always check a cached file is still available before using it.

Example::

  var checkCachedLogo = function () {
    forge.prefs.get("logo-cache", function (file) {
      if (!file) {
        // Logo never cached
        cacheLogo();
        return;
      }
      forge.file.isFile(file, function (isFile) {
        if (!isFile) {
          // File no longer available
          cacheLogo();
        } else {
          // Logo available
          showCachedLogo(file);
        }
      });
    });
  }

Using a cached file
~~~~~~~~~~~~~~~~~~~

Finally we need to be able to display a cached file, to do that we can use the following code:

Example::

  var showCachedLogo = function (file) {
    forge.file.URL(file, function (url) {
      var logo = document.createElement('img');
      logo.src = url;
      document.body.appendChild(logo);
    });
  }
  
Complete example
~~~~~~~~~~~~~~~~

Putting those functions together we get an example which will cache a logo and display it from the cache:

Example:

.. code-block:: html

  <!DOCTYPE html>
  <html>
    <head>
    </head>
    <body>
      <h1>Hello caching world!</h1>
      <script>
        var showCachedLogo = function (file) {
          forge.file.URL(file, function (url) {
            var logo = document.createElement('img');
            logo.src = url;
            document.body.appendChild(logo);
          });
        }
        
        var cacheLogo = function () {
          forge.file.cacheURL("https://trigger.io/forge-static/css/trigger/f/logo-header-small-forge.png", function (file) {
            // File cached save the file object for later
            forge.prefs.set("logo-cache", file, function () {
              // Logo saved
              showCachedLogo(file);
            });
          });
        }
        
        var checkCachedLogo = function () {
          forge.prefs.get("logo-cache", function (file) {
            if (!file) {
              // Logo never cached
              cacheLogo();
              return;
            }
            forge.file.isFile(file, function (isFile) {
              if (!isFile) {
                // File no longer available
                cacheLogo();
              } else {
                // Logo available
                showCachedLogo(file);
              }
            });
          });
        }
        
        checkCachedLogo();
      </script>
    </body>
  </html>

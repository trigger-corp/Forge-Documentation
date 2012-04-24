.. _tools-proxy:

Working behind a Proxy
======================

With the forge command line tool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If you're having trouble running the tools behind a proxy server, you can
modify ``forge_build.json`` in the directory where you installed the forge
tools to look like:

.. parsed-literal::
  {
    "main": {
        "server": "https://trigger.io/api/",
        "proxies": {
            "https": "my.proxy.com:8080"
        }
    }
  }

.. note:: Make sure to specify the proxy for **https** as all traffic to our services is over https.

With the Trigger Toolkit
~~~~~~~~~~~~~~~~~~~~~~~~

As above, you need to modify ``forge_build.json`` to use a proxy for all https traffic. The location of this depends on your operating system:

*On Windows Vista/7*
    C:\\Users\\<Your User>\\AppData\\Local\\Trigger Toolkit\\build-tools\\forge_build.json

*On Windows 2000/XP*
    C:\\Documents and Settings\\<Your User>\\Local Settings\\Application Data\\Trigger Toolkit\\build-tools\\forge_build.json

*On OS X*
    <your home directory>/Applications/TriggerToolkit.app/Contents/MacOS/build-tools/forge_build.json

*Using the Python distribution*
    <path to the Trigger Toolkit>/build-tools/forge_build.json

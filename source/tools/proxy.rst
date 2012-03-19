.. _tools-proxy:

Working behind a Proxy
======================
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

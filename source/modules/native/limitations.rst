.. _native_plugins_limitations:

Limitations of native plugins
=============================

Native plugins are still a beta feature for Forge, and they still have some limitations which we plan to address in the future:

* Currently native code can only be triggered by Javascript, not by native events, such as receiving a push notification, or registering a URL handler.
* Native plugins cannot currently edit the Android app manifest to add permissions or services, or register its own URL handlers on either platform.

.. important:: If you need more functionality to develop your native plugin please let us know what you require by emailing support@trigger.io.
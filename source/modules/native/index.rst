.. _native_plugins:

Native plugins
==============

.. important:: Plugins are currently a beta feature, get in touch with support@trigger.io if you're interested in trying them out.

Native plugins allow you to write native Android and iOS code, compile it and include this compiled code in your app built using Forge. As part of this it also provides a method for your native code to communicate with your Javascript code.

Writing native plugins is obviously different for Android and iOS, however we have tried to keep the experience as consistent as possible. With that in mind these docs are split into the various tasks you might want to complete as part of writing a native plugin, with instructions for Android and iOS included in each section.

.. toctree::

    the_basics
    api_methods
    javascript_events
    native_events
    native_communication
    external_libraries
    native_build_steps
    including_resources
    api_docs
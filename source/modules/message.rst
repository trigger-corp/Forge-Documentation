.. _modules-message:

``message``: Component communication
====================================
**Platforms: Browser only**

It is often useful to be able to send and receive messages between components of your extension. To achieve this in a cross-browser manner, use these methods to broadcast and listen for messages.

Config
------

The ``message`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "message": true
        }
    }

API
---

``listen``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sets up a handler function which will receive messages sent ("broadcast") by your extension.

By supplying the optional *type* parameter, you can filter the messages on which your callback will be invoked; see the *type* parameter to the :ref:`broadcast <api-broadcast>` and :ref:`broadcastBackground <api-broadcastBackground>` methods. If the *type* parameter is omitted, your callback will be invoked for all broadcast messages.

The *callback* parameter will be invoked when a message is to be delivered, with the message contents as its first parameter and a "reply function" as its second parameter. The "reply function" is used to send responses back to the code which broadcast the original message.

.. js:function:: message.listen([type, ]callback, error)

    :param string type: (optional) if included, the callback will only be fired for messages broadcast with the same type; if omitted, the callback will be fired for all messages
    :param function(content,reply) callback: will be called with the contents of relevant broadcast messages as its first parameter and a reply function as its second parameter
    :param function(content) error: called with details of any error which may occur

.. _api-broadcast:

``broadcast``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Sends a message to be received by other components of your extension. Messaging will not be recieved by the background page.

The *type* parameter can be used to indicate the purpose of the message and limit the active listeners which will receive the message.

The *callback* parameter will be invoked with any responses from listeners; it may be called multiple times, depending on whether your listeners use the "reply function".

.. js:function:: message.broadcast(type, content, callback, error)

    :param string type: limits the listeners which will receive this message
    :param any content: the message body
    :param function(content) callback: invoked each time a listener returns a response to the broadcaster, with the response as its only argument
    :param function(content) error: called with details of any error which may occur

.. _api-broadcastBackground:

``broadcastBackground``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

**Restrictions: Not available from the background page**

Sends a message to be received by listeners in your background code: similar to :ref:`broadcast <api-broadcast>`, except that listeners created in individual browser pages will not receive this message; only listeners created in your background page (see :ref:`extension-concept-background`).

.. js:function:: message.broadcastBackground(type, content, callback, error)

    :param string type: limits the listeners which will receive this message
    :param any content: the message body
    :param function(content) callback: invoked each time a listener returns a response to the broadcaster, with the response as its only argument
    :param function(content) error: called with details of any error which may occur

``toFocussed``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Browser only**

Like :ref:`broadcast <api-broadcast>`, this method sends a message to be received by content script listeners.

However, not all listeners are passed the message: only the currently focused tab's listeners will receive this message. If the currently focussed tab is not displaying a page your add-on has activated on, no listeners will receive this message.

The callback may be invoked a number of times if several message listeners have been set up per page.

.. js:function:: message.toFocussed(type, content, callback, error)

    :param string type: limits the listeners which will receive this message
    :param any content: the message body
    :param function(content) callback: invoked each time a listener returns a response to the broadcaster, with the response as its only argument
    :param function(content) error: called with details of any error which may occur
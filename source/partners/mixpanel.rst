.. _mixpanel:

Mixpanel
===============================================================================
Mixpanel is a real-time analytics service that can help you understand how users interact with your application.
See the `Mixpanel <http://www.mixpanel.com>`_ home page to find out what sort of functionality is provided and how the specific API is used.

``mpq``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: All**

**Restrictions: Not available in content scripts**

Including Mixpanel in your browser extension or mobile application is done by modifying the configuration file.
Add the following properties::

	"partners": {
		"mixpanel": {"token": "your project token here"}
	}

Replace "your project token here" with the unique token generated for your project in Mixpanel.

To see an example using Mixpanel tracking in a Chrome extension :ref:`click here<partners-mixpanel-demo>`
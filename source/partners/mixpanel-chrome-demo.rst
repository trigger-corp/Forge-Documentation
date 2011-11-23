.. _partners-mixpanel-demo:

Mixpanel Demo
============================================================================================================
This tutorial will show how simple it is to add Mixpanel tracking to your browser extension using Forge.
We will develop a simple browser extension that appends an icon to the browser's toolbar which opens a pop-up page when clicked.
This page will contain a single button which will send Mixpanel tracking event.

.. _chrome-mixpanel-download:

To get started first download some resources needed for this tutorial

Pop-up Page
-----------
We need to create an html file that will be displayed as the pop-up when the icon is clicked

* Create a file popup.htm and add the basic html tags. It should look something like:

.. code-block:: html

    <html>
      <head>
      </head>
      <body>
      /body>
    </html>

* We will use jquery to set up a button click handler. Append the jquery script tag in the head element :

.. code-block:: html

	<script type="text/javascript" src="jquery.min.js"></script>

* In the body element add a button :

.. code-block:: html

	<input id="myButton" type="button" value="Click Me">

* Next append another script tag to the head element following jQuery::

	<script type="text/javascript">
	$('#myButton').live('click', function(){
		forge.partner.mpq.track('My Button Clicked');
	});
	</script>

All we've pretty much done here is create a button element inside the html.
When the page loads it will run the code inside of the WebMynd wrapper, which simply adds a click listener to the button.
When the button is clicked the code inside the handler executes and uses Mixpanel API to track a "My Button Clicked" event

Configuration file
--------------------
All that is left to do now is to plug in the pop-up page to display and configure Mixpanel.

* Open up webmynd_configuration.json that was included in the package you :ref:`downloaded<chrome-mixpanel-download>` for this tutorial
* Replace "your pop-up page relative url" with the relative url for the html page you've created ::

	"browser_action": {
		"default_popup": "popup.html"
	},

* Next replace "your mixpanel project token" with the token generated for your project by Mixpanel ::

	"partners": {
		"mixpanel": {"token": "your token here"}
	}

Running
-------
Build your extension using Forge and load the extension into the browser. An "m" icon should appear on the browsers menu.
When clicked a pop-up opens up with a click me button. When this button is clicked it will track a Mixpanel "My Button Clicked" event.



.. _best-practice-local:

Referencing local resources
================================================================================

Forge supports building apps that work offline. The HTML, CSS and JavaScript code you write is packaged locally with your app and you can also include image and :ref:`media<modules-media>` assets locally.

Here we discuss how to reference your local assets from your code. You can also read about :ref:`how to download and cache files<forge-cache>` after the initial install.

Relative URLs
~~~~~~~~~~~~~~

You should always use relative URLs when referencing resources. For example, with this directory structure for your ``src`` directory::

    config.json
    identity.json
    index.html

    css/
    	style.css

    img/
    	trigger-io-forge-small.png

    js/
    	jquery-1.7.1.min.js
    	main.js

You should reference the image from your ``index.html`` like this::

    <img id="image" src="img/trigger-io-forge-small.png" />

Similarly, you could set it as background image for an element by adding this to your ``style.css``::

	#background {
		height: 46px;
		background: url('../img/trigger-io-forge-small.png');
	}

We've used an image in our examples here but you can reference other assets from the HTML (like JavaScript styles and CSS stylesheets) in the same way.
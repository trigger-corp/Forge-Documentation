.. _best-practice-local:

Referencing local resources
================================================================================

Forge supports building apps that work offline. The HTML, CSS and JavaScript code you write is packaged locally with your app and you can also include image and :ref:`media<modules-media>` assets locally.

Here we discuss how to reference your local assets from your code. You can also read about :ref:`how to download and cache files<forge-cache>` after the initial install.

Considerations
~~~~~~~~~~~~~~~~~

You can reference local resources using relative or absolute urls. 

Relative urls are the simplest way to reference assets. However, if you add new assets using :ref:`Reload<modules-reload>` then you must use absolute urls because of the way the local filesystem is organized.

Relative URLs
~~~~~~~~~~~~~~

You can use relative urls in the same way you would on the web. For example, with this directory structure for you ``src`` directory::

    config.json	identity.json	index.html

    css:
    style.css

    img:
    trigger-io-forge-small.png

    js:
    jquery-1.7.1.min.js	main.js

You could reference the image from your ``index.html`` like this::

    <img id="image" src="img/trigger-io-forge-small.png" />

Similarly, you could set it as background image for an element by adding this to your ``style.css``::

	#background {
		height: 46px;
		background: url('../img/trigger-io-forge-small.png');
	}

We've used an image in our examples here but you can reference other assets from the HTML (like JavaScript styles and CSS stylesheets) in the same way. 


Absolute URLs
~~~~~~~~~~~~~~~~~~~~~~~

You must always use absolute URLs when you change assets with :ref:`Reload<modules-reload>`. 

To get absolute URLs for assets, you must use the :ref:`tools.getURL<tools-getURL>` API. Using that API, you will need to set the absolute path in the style or ``src`` attribute of an element from JavaScript.

For example, this code snippet shows how to construct an absolute url for your asset and then use it by updating DOM element attributes or styles to reference it::

    forge.tools.getURL('', function(baseURL){
	
	    var absoluteURL = baseURL + 'img/trigger-io-forge-small.png';
	
	    $('#background').css({
		    background: 'url("'+absoluteURL+'")'
	    });
	
	    $('#image').attr('src', absoluteURL);
	
    });


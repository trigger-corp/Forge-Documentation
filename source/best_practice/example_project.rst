.. _best-practice-example_project

Example Project
===============

Putting all these concepts into practice, we've developed
a little example project with a css reset, backbone and a couple of pages with transitions.
Please feel free to base your own projects on this - it's a great springboard for a new project.

Features:

* Backbone.js
* Css reset
* Rss feed parsing
* Transitions

Overview
--------

The entry point for the application is in index.html, ``$(Demo.init)`` calls ``init()``,
defined in demo.js::

	init: function () {
		Demo.Utils.parseRSS(rss_url, function(data) {
			Demo.router = new Demo.Router();
			Demo.feeds = new Demo.Collections.Items(data.entries);
			Backbone.history.start();
		});
	}

The inner three lines are the most important here (they are just wrapped in
``parseRSS()`` to get the rss feed). First we create the router::

	Demo.router = new Demo.Router();
	
This is the backbone of... backbone. The router is where the urls are defined,
and handed over to the view code.

the ``Demo.Collections.Items`` collection is defined in models.js as::

	Demo.Models.Item = Backbone.Model.extend();
	
	Demo.Collections.Items = Backbone.Collection.extend({
		model: Demo.Models.Item
	});

Simply a collection of Item models, easy enough! In the context of
``Demo.Utils.parseRSS(rss_url, function(data) {``, data is our rss object, with
``data.entries`` 
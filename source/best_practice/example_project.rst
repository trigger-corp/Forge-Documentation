.. _best-practice-example_project:

Example Project
===============

Putting all these concepts into practice, we've developed
a little example project with a CSS reset, Backbone and a couple of pages with transitions.

Please feel free to base your own projects on this - it's a great springboard for a new project.

Features:

* Backbone.js
* CSS reset
* RSS feed parsing
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
``parseRSS()`` to get the RSS Feed). First we create the router::

    Demo.router = new Demo.Router();

This is the backbone of... Backbone. The router is where the urls are defined,
and handed over to the view code.

The ``Demo.Collections.Items`` collection is defined in models.js as::

    Demo.Models.Item = Backbone.Model.extend();
    
    Demo.Collections.Items = Backbone.Collection.extend({
        model: Demo.Models.Item
    });

Simply a collection of Item models, easy enough! In the context of
``Demo.Utils.parseRSS(rss_url, function(data) {``, data is our RSS object, with
``data.entries`` 

``Backbone.history.start()`` kicks off backbone's window.onhashchange event subscribtion.
If the browser doesn't support onhashchange, it monitors window.location periodically.
When the url changes, the routes defined in ``routes.js`` are used::

    routes: {
        "" : "index",         // entry point
        "item/:item_id":"item"// #item/id
    },

lets say the user visits /, the routes run index()::


    index: function() {
        var index = new Demo.Views.Index({
            collection: Demo.feeds,
            back      : false
        });
        index.show();
    },
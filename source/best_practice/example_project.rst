.. _best-practice-example_project:

Example Project
===============

We've developed a little example project with a CSS reset,
Backbone and a couple of pages with transitions.

Features
--------

* Backbone.js
* CSS reset
* RSS feed parsing
* Transitions

Please feel free to base your own projects on this - it's a great springboard for a new project.
The code is hosted on github here: https://github.com/trigger-corp/Forge-Bootstrap

Included files
..............

We're using the css reset from `html5boilerplate.com <http://html5boilerplate.com>`_
to keep things sane. For mobile development, jQuery can be a quite heavyweight
so we've included `Zepto <http://zeptojs.com/>`_, a "minimalist JavaScript framework for modern web browsers" We've found that it's a great jQuery-inspired js framework.

We use Zepto throughout the views in the tutorial.

Lets get stuck in
-----------------

The entry point for the javascript application is in index.html, ``$(Demo.init)`` calls ``init()``,
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
``parseRSS()``, data is our RSS object, with
``data.entries`` being an array of entries, which we pass into the collection to
wrap with underscore.js's
`excellent <http://documentcloud.github.com/underscore/#collections>`_
functions for working with collections of data.

``Backbone.history.start()`` kicks off backbone's window.onhashchange event subscribtion.
If the browser doesn't support onhashchange, it monitors window.location periodically.
When the url changes, the routes defined in ``routes.js`` are used::

    routes: {
        "" : "index",         // entry point
        "item/:item_id":"item"// #item/id
    },

lets say the user visits /, the router calls index()::


    index: function() {
        var index = new Demo.Views.Index({
            collection: Demo.feeds,
            back      : false
        });
        index.show();
    },

This function creates an ``Index`` view, passing in our feeds collection
(that we created back in ``init()``) and a boolean describing the direction of the animation.
Becuase ``Index`` extends ``Page``, we can use the ``show()`` function,
which we'll look at after looking at the ``index`` view.

Index View
----------

The index view looks like this::

    Demo.Views.Index = Demo.Views.Page.extend({
    
        initialize: function() {
            this.render();
        },
    
        render: function() {
            var that = this;
            this.collection.each(function(feed_item, index){
                if (index % 2 === 1) {
                    var new_view = new Demo.Views.Feed({
                        model: feed_item,
                        odd: true}
                    );
                } else {
                    var new_view = new Demo.Views.Feed({
                        model: feed_item,
                        odd: false
                    });
                }
                $(that.el).append(new_view.el);
            });
            return this;
        }
    });
	
The entry point for every view is the ``initialize()`` function,
which we use to kick of our ``render()`` function.
``render()`` iterates through each item in the collection,
creating a ``Feed`` view for each, and appends it to the ``Index`` view's el.

Because we used ``Page's`` ``show()`` function, we'd better look at that too::

Page View
---------
::

    Demo.Views.Page = Backbone.View.extend({
        className: "page",
    
        initialize: function () {
            this.render();
        },
        show: function () {
            direction_coefficiant = this.options.back? 1 : -1
            var el = this.el;
            if ($('.page').length) {
                var $old = $('.page').not(el);
				
                $old.get(0).style["margin-left"] = ""
                $old.get(0).style["-webkit-transform"] = ""
				
                $(el).appendTo('body').hide();
                $(el).show().css({"margin-left": 320 * direction_coefficiant});
                $(el).anim({translate3d: -320 * direction_coefficiant +'px,0,0'}, 0.3, 'linear');
                $old.anim({translate3d: -320 * direction_coefficiant + 'px,0,0'}, 0.3, 'linear', function() {
                    $old.remove();
                });
            } else {
                $(el).appendTo('body').hide();
                $(el).show();
            }
            window.scrollTo(0, 0);
        }
    });

``pages`` are indended to be ``extend()`` ed by views, the ``show()`` function handles the business of animating the new element over the old
and removing the old when it is done.

Our ``index`` view creates a new ``Feed`` view for each iteam in the collection,
and appends it to the page element.

Feed view
---------
::

    Demo.Views.Feed = Backbone.View.extend({

        events: {
            //TODO: click is sub-optimal on phones, use forge.is to use tap on phones
            "click .feed-even": "expand_item",
            "click .feed-odd" : "expand_item"
        },

        expand_item: function () {
            console.log(this.model.cid);
            Demo.router.navigate("item/" + this.model.cid.split("").slice(1), true);
        },

        initialize: function() {
            this.render();
        },    

        render: function() {
            var feed_class = (this.options.odd? "feed-odd" : "feed-even");
            $(this.el).append('<div class="' + feed_class + '">' +
                                this.model.get("title") +
                                "</div>");
            return this;
        },
    });

The ``Feed`` view simply formats each item's title nicely, binding a ``click`` event
to navigate the user to the ``/item/`` page.

When the user naviages to ``/item/[id]`` (where id is the index of the collection)
the router passes ``[id]`` to ``item()``:: 

    item: function(item_id) {
            var item = new Demo.Models.Item(Demo.feeds.models[item_id]);
            var item_view = new Demo.Views.Item({
                model: item,
                back : true
            });
            item_view.show();
    }

``Item`` is a very simple view that grabs title and date from the model and displays them nicely. Note that we're passing in the ``back``
bool, which ``Page`` uses to work out which way the page should slide in.
``Item`` is reproduced here for clarity

Item View
---------

::

    Demo.Views.Item = Demo.Views.Page.extend({
    
        events: {
            //TODO: click is sub-optimal on phones, use forge.is to use tap on phones
            "click #back": "go_back"
        },
    
        expand_item: function () {
            forge.tabs.open(this.model.get("link"));
        },
    
        initialize: function() {
            this.render();
        },
    
        go_back: function() {
            Demo.router.navigate("", true);
        },
        
        render: function() {
            var author = this.model.get("author");
            var author_line = (author ? " by " + author : "");
    
            $(this.el).append('<div id="back", class="feed-even">Back</div>');
            
            $(this.el).append('<li class="feed-odd">' +
                                this.model.get("title") +
                                '<div class="author">' +
                                    author_line +
                                '</div>' +
                                '<div class="date">' +
                                    this.model.get("publishedDate").split(" ").slice(0, -1).join(" ") +
                                '</div>' +
                              '</li>');
            return this;
        }
    });

In ``expand_item()``, we are using ``forge.tabs.open()`` to open a new tab in
a cross-platform manner. Our documentation for ``open()`` is :ref:`here <tabs-management>`.

That's it
---------

Play with the source for yourself, we hope everything is clear.

Still unsure? Want to ask for help? Spotted a mistake in this tutorial? Drop us a line at support@trigger.io and we'll be happy to help.
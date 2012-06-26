.. _gmaps:

.. highlight:: js
   :linenothreshold: 5

GMaps for location-based apps
===============

We've developed a little example project, using a CSS reset,
Backbone.js and a couple of pages with transitions.

This project will show you how to:

* include your JavaScript files in your app
* use Backbone.js to present a responsive interface
* use a CSS reset
* implement an example transition between views in your app

Please feel free to base your own projects on this - it's a great springboard for a new project.
The code is hosted on github here: https://github.com/trigger-corp/Forge-Bootstrap

Included files
--------------------------------------------------------------------------------

* `Backone.js <http://documentcloud.github.com/backbone/>`_ to handle history, user actions, and to structure our JavaScript in general
* `HTML5 Boilerplate <http://html5boilerplate.com>`_ to reduce the impact of inconsistent rendering defaults on different platforms
* `Zepto <http://zeptojs.com/>`_, a light-weight, mobile-focussed alternative to jQuery, for DOM manipulation

Let's get stuck in
------------------

To work with your JavaScripts and CSS in the app, just include them in your index.html as you might in a normal website:

.. code-block:: html

    <link rel="stylesheet" href="css/reset.css">
    <link rel="stylesheet" href="css/demo.css">

    <script type="text/javascript" src="js/lib/zepto.min.js"></script>
    <script type="text/javascript" src="js/lib/underscore-min.js"></script>
    <script type="text/javascript" src="js/lib/backbone-min.js"></script>
    <script type="text/javascript" src="js/demo.js"></script>

Here, we have simply used the HTML5 Boilerplate reset (``reset.css``), JavaScript libraries and two of our own files, ``demo.css`` and ``demo.js``.

It's best to have one entry point for your application, with other included
JavaScript files being just libraries, containing functions and objects. When using Backbone, your entry point should set up whatever your app requires to function, then start Backbone's history system.

For example, in this project, we use ``$(Demo.init)`` to run the following function once, at app startup::

    // Called once, at app startup
    init: function () {
        // Grab the Trigger twitter feed
        forge.request.ajax({
            url: "https://twitter.com/statuses/user_timeline/14972793.json",
            dataType: "json",
            success: showIndex
        });

        // to be called once we have the Trigger twitter feed
        function showIndex(data) {
            // Save away initial data
            Demo.items = new Demo.Collections.Items(data);

            // Set up Backbone
            Demo.router = new Demo.Router();
            Backbone.history.start();
        }
    }

Here we're using the `Trigger twitter feed <http://twitter.com/#!/triggercorp>`_ as example data to work with: we use our :ref:`request.ajax <request_ajax>` function to retreive our tweets, store the data into a collection then start Backbone.

Using Backbone.js
-----------------

``Backbone.history.start()`` kicks off Backbone's ``window.onhashchange`` event subscription.
When the `fragment <http://en.wikipedia.org/wiki/Fragment_identifier>`_ of the URL changes, the routes defined in ``routes.js`` are used::

    routes: {
        "" : "index",         // entry point: no hash fragment or #
        "item/:item_id":"item"// #item/id
    },

The routes map a URL to a function. We have two routes defined here: one that
matches ``#`` (or URLs with no hash fragment) and invokes ``index()``, and one that matches ``#item/[item_id]``.
``item_id`` is then passed into ``item()`` as a parameter. Routes map out the URLs for your whole
app.

Using Backbone to manage views inside a Forge app is a great strategy: not only do we build URLs in the history stack (meaning the back button works as expected on Android, for example), we are also able to take complete control over what is displayed in the app, without having to resort to sluggish page loads.

However, especially on mobile platforms, your users will expect some form of dynamic transition from one view to the next; to do that, you can organise your Backbone views into pages.

Page View
---------
This snippet shows how we implement pages in this project, with an animated transition as one page becomes active. You can also see us using Zepto for DOM manipulation here.

::

    Demo.Views.Page = Backbone.View.extend({
        className: "page",

        initialize: function () {
            this.render();
        },
        show: function () {
            $('.page').css({"position": "absolute"});
            var direction_coefficient = this.options.back? 1 : -1;
            if ($('.page').length) {
                
                var $old = $('.page').not(this.el);
                
                //This fix was hard-won, just doing .css(property, '') doesn't work!
                $old.get(0).style["margin-left"] = ""
                $old.get(0).style["-webkit-transform"] = ""
                
                this.$el.appendTo('body').hide();
                this.$el.show().css({"margin-left": 320 * direction_coefficient});
                this.$el.anim({translate3d: -320 * direction_coefficient +'px,0,0'}, 0.3, 'linear');
                $old.anim({translate3d: -320 * direction_coefficient + 'px,0,0'}, 0.3, 'linear', function() {
                    $old.remove();
                    $('.page').css({"position": "static"});
                });
            } else {
                this.$el.appendTo('body').hide();
                this.$el.show();
            }
            window.scrollTo(0, 0);
        }
    });

You can ``extend()`` this page in your own views if you wish, and use the ``show()`` method to switch from one to another.

For example, in this project, we create a page for the initial view of all the tweets, and a page for each individual tweet when the user selects it.

Using other parts of the Forge API
--------------------------------------------------------------------------------
We have already seen the use of ``forge.request.ajax`` to easily make a request to a remote server. This project makes use of some other Forge APIs too.

In ``expand_item()``, we use ``forge.tabs.open()`` to open an external page new tab in a cross-platform manner. Our documentation for ``open()`` is :ref:`here <modules-tabs>`.

Lastly, we use ``forge.is`` in the ``click_or_tap()`` function so that we can listen for tap events on mobile devices, but click events otherwise. Documentation for easy platform detection can be found here :ref:`forge.is.mobile <modules-is>`

::

    click_or_tap: function(obj) {
        //for property in obj, add "click " to property and use original value
        var new_obj = {};
        for(var property in obj) {
            if (obj.hasOwnProperty(property)) {
                if (forge.is.mobile()) {
                    new_obj["tap " + property] = obj[property];
                }
                else {
                    new_obj["click " + property] = obj[property];
                }
            }
        }
        return new_obj
    }

This is important because the ``click`` event is less responsive on mobile than
``tap``.

That's it
---------

Play with the source for yourself, we hope everything is clear.

Still unsure? Want to ask for help? Spotted a mistake in this tutorial? Drop us a line at support@trigger.io and we'll be happy to help.

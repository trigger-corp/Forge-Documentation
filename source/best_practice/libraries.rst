.. _best-practice-libraries

Using Javascript libraries
==========================

It is important to remember that Forge apps are just HTML5/JS apps, this means they can take advantage of the vast library of Javascript tools and libraries which are freely available. This page lists some of the libraries we find most useful and some tips when using them.

In general (on mobile apps especially) reducing memory usage is important, and using the minimal number of frameworks and ensuring minified versions are always used can improve performance.

jQuery/Zepto
------------

* jQuery is one of the most popular Javascript frameworks and can simplify a number of common Javascript tasks. On mobile however jQuery is a fairly large library and can cause performance issues, and it may be preferable to use Zepto.
* Zepto is a lightweight version of jQuery aimed at mobile browsers, it lacks some less used jQuery features, but is highly mobile optimised and much smaller.
* See http://zeptojs.com/

iScroll
-------

* Creating fixed position or ``overflow: scroll`` elements is not possible in the vast majority of mobile browsers currently, iScroll recreates this effect in Javascript.
* Unfortunately this means it can be less efficient than native scrolling would be, so this library should be used with caution. If possible pages which are designed with no fixed header/footer will often run much more smoothly than a more complex page.
* See http://cubiq.org/iscroll-4

Backbone
--------

* Backbone is a lightweight and increasingly popular way of organising your Javascript code. Similar to the concepts of MVC Backbone separates out the sections of your code and provides helpful functions for doing common tasks to do with organising and handling data.
* See http://documentcloud.github.com/backbone/
.. _facenote-tutorial-3:

Tutorial Part 3
===========================================================================

In the final part of this tutorial, we build on Part II to improve the appearance and functionality of the notes interface.

.. contents::
   :backlinks: none

Goal
----
By the end of this part of the tutorial, your Facebook notes application will look much more appealing than before!

Making the note look nicer
--------------------------
Rather than just a plain, unstyled textarea, let's make the note more appealing by having it look a bit like a Post-It note.

To do this, we'll need to embed a CSS file in the Facebook page to style our note. In ``src/config.json``, change the ``styles`` array from::

  "styles": [
  ],

to::

  "styles": [
    "/fb-note-demo.css"
  ],

.. highlight:: css

In the same folder as ``fb-note-demo.js``, create ``fb-note-demo.css`` with the following content::

  .fb-note  {
    background-color: #FEF49C;
    border: 1px solid #CEC46C;
    position: absolute;
    top: 10px;
    right: 10px;
    z-index:1000;
    -moz-box-shadow: 5px 5px 5px #555;
    -webkit-box-shadow: 5px 5px 5px #555;
    box-shadow: 5px 5px 5px #555;
  }

  .fb-note a.save-note {
    display: block;
    font-size: 140%;
    width: 280px;
    background-color: white;
    margin: 0px auto;
    text-align: center;
    margin-bottom: 3px;
    background-color: #EEEEFF;
  }

  .fb-note .fb-note-content {
    width: 280px;
    height: 170px;
    border: none;
    background-color: transparent;
  }

.. highlight:: js

Feel free to change this CSS as you see fit!

Reload a Facebook profile page, and your note should be a bit nicer to look at!

Adding a close button
---------------------
Now that the note is covering some of the page, we should really add a close button to let people temporarily hide it. Of course, in a real application, this setting should be persisted, and more complex show/hide functionality considered, but for this demo a simple approach is fine.

When building the note in your JavaScript, change ``noteEl`` to be::

    var noteEl = $("<div class='fb-note' style='z-index: 1000; position: absolute'>"+
      "<a class='fb-close-note'>X</a>"+
      "<textarea class='fb-note-content'></textarea>"+
      "<a class='save-note'>save note</a>"+
      "</div>");

Then add a ``click()`` handler for the close button to the end of your ``forge.prefs.get`` callback::

  $("a.fb-close-note", noteEl).click(function() {
    $(".fb-note").remove();
  });


.. highlight:: css

Finally, add some CSS styling for the close button in ``fb-note-demo.css``::

  .fb-note a.fb-close-note {
    float: right;
    color: red;
    font-weight: bold;
  }

Reference extension
-------------------
`fb-part-2.zip <../_static/facenote/fb-part-2.zip>`_ contains the code you should have at the end of this tutorial. Feel free to check your code against it, or build on it to improve the Facebook note demo add-on!

It's not working!
-----------------
* if there's a problem with your CSS not being applied properly, check that you can access the stylesheet at the URL specified in ``src/config.json``
* for JavaScript problems, setting a debugger breakpoint at the start of your *onLoad* function is often the best place to start.
* are you seeing the wrong note for people? It's due to Facebook's strange page transitions: reloading the page should show the right note. In a real application, you could add a simple poller on ``document.URL``.

.. note:: ``api.log(message)`` is a useful function which outputs messages to the console; we find it much more convenient than having ``alert()`` calls everywhere!

Other useful functions
----------------------
This tutorial has not covered all of the API Forge exposes to your extensions: see the :ref:`api` documentation for a comprehensive list.
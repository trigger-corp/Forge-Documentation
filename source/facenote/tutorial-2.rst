.. _facenote-tutorial-2:

Tutorial Part 2
========================================================================

In the second part of this tutorial, we build on the previous steps to add the JavaScript code which lets users attach text notes to profiles on Facebook.

.. contents::
   :backlinks: none

Goal
----
By the end of this part of the tutorial, you will have a basic extension which lets users attach notes to Facebook profiles.

Identifying a Facebook profile
-----------------------------------
**Goal: only show an alert when we're on a Facebook profile page**

To show the correct note on each Facebook profile page, we will use a regular expression to pull the user ID out of a Facebook URL.

Facebook profile page URLs take two forms::

* ``www.facebook.com/profile.php?id=123456789``
* ``www.facebook.com/profile.name``

If we're not on a page that has a URL like this, we don't want to do anything.

Replace your alert with::

  var oldProfile = new RegExp("\\.facebook\\.com/profile\\.php\\?id=(\\d+)");
  var newProfile = new RegExp("\\.facebook\\.com/([A-Za-z0-9\\.]+)(\\?.+)?$");
  var ignoreProfiles = new RegExp("\\.php$");
  
  var oldProfileM = oldProfile.exec(document.URL),
    newProfileM = newProfile.exec(document.URL),
    personID = undefined;
  if (oldProfileM) {
    // URL is like www.facebook.com/profile.php?id=123456789
    var personID = oldProfileM[1];
  } else if (newProfileM) {
    // URL is like www.facebook.com/profile.name ...
    var personID = newProfileM[1];
    if (ignoreProfiles.exec(personID)) {
      // ... but it's a system page (like the login screen)
      var personID = undefined;
    }
  }
  
  if (typeof personID !== "undefined") {
    handleProfilePage(personID);
  }
  
  function handleProfilePage(personID) {
    alert("On a Facebook profile page");
  }

We've used a regular expression which matches URLs like http://www.facebook.com/profile.php?id=123456789 to only continue with our code if we appear to be on a profile page. It also pulls out the unique user ID which we will soon use to attribute the right note to the right person - we save the unique ID into the ``personID`` variable.

.. _read-pref-tut:

Reading in existing notes
-------------------------
Of course, we want to save notes away so that we can see them again next time we visit a profile page. To do that, we will use a feature of the Forge platform which lets us persist data between browser windows and across page loads and browser restarts; we call these data :ref:`preferences <preferences>`.

To read a preference, we will use the :ref:`forge.prefs.get <api-prefs-get>` method in ``fb-note-demo.js``: add the following code inside the to the end of the ``handleProfilePage`` function::

  forge.prefs.get("fb_notes", function(notes) {
    // set to null when no preference yet set
    var existingNotes = notes === null? {}: notes;
    
    if (existingNotes[personID] === undefined) {
      existingNotes[personID] = "";
    }
  });

As :ref:`forge.prefs.get <api-prefs-get>` is an asynchronous method, we have passed in a callback to process the stored value.

.. note:: The check for ``existingNotes`` being ``null`` is to handle the initial case where there are no persisted notes.

.. _change-note-tut:

How do users change the note?
-----------------------------
Now we can read in existing notes, but how do we let users edit them?

Well, to do this we will create a small HTML snippet to be inserted into the Facebook page, which lets users edit the note. Add this code to the end of the ``forge.prefs.get`` callback::

  var noteEl = document.createElement("div"),
    textarea = document.createElement("textarea");
  noteEl.appendChild(textarea);
  document.body.insertBefore(noteEl, document.body.firstChild);

Rebuild your app with ``forge build``, reload the extension and on profile pages you should now see a ``<textarea>`` inserted right at the top of the page. We will cover how to *save* the note in a short while.

Using jQuery instead of plain JavaScript
----------------------------------------
Interacting with the DOM can be a bit cumbersome in plain JavaScript: for this reason, you may want to include third-party libraries in your extension. To do so, we'll just change ``src/config.json`` to include jQuery in the list of scripts we include when the extension activates.

First, download http://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js to your ``src`` directory, then update your ``src/config.json``::

    "scripts": ["jquery.min.js", "/fb-note-demo.js"]

So, we can replace the code from :ref:`the previous section <change-note-tut>` with this (adding a couple of element classes)::

    var noteEl = $("<div class='fb-note' style='z-index: 1000; position: absolute'>"+
      "<textarea class='fb-note-content'></textarea>"+
      "</div>");
    $(".fb-note-content", noteEl).val(existingNotes[personID]);
    $("body").first().prepend(noteEl);

.. _write-pref-tut:

Saving the note
---------------
At this point, you should see a ``textarea`` at the top of Facebook profile pages. Next, we need to be able to save the contents of that textarea, so that the notes are persisted between page loads and browser restarts.

First, change the ``noteEl`` element to include a **save** link::

    var noteEl = $("<div class='fb-note' style='z-index: 1000; position: absolute'>"+
      "<textarea class='fb-note-content'></textarea>"+
      "<a class='save-note' style='display:block'>save note</a>"+
      "</div>");

Then add a ``click()`` handler to that link::

    $("a.save-note", noteEl).click(function() {
      // save textarea content into the existingNotes object we read before
      existingNotes[personID] = $(".fb-note-content", noteEl).val();
      // forge.prefs.set is the inverse of forge.prefs.get
      forge.prefs.set("fb_notes", existingNotes);
      alert("Note saved!");
    });

Bringing it together
--------------------
Now, when you go to a Facebook profile page, you should see a ``textarea`` at the top of the page, along with a **save note** link. Editing the text and saving it should pop up an alert box - and the next time you visit that profile page, the saved message should be displayed.

You should be able to save different notes for different people.

Reference extension
-------------------
`fb-part-2.zip <../_static/facenote/fb-part-2.zip>`_ contains the code you should have at this point. Feel free to check your code against it, or use it to resume the tutorial from here.

It's not working!
-----------------
* You can use the standard Chrome JavaScript debugger to check for logic problems in your code
* JavaScript files can be cached, clear this out at ``chrome://history/#e=1&p=0``
* are you seeing the wrong note for people? It's due to Facebook's strange page transitions: reloading the page should show the right note. In a real application, you could add a simple poller on ``document.URL``
* if your JavaScript file has not been embedded in the page (i.e. you don't see it in the list of available scripts in the debugger), there's either a syntax error in your file (which will show up on the console) or there's a problem reading the file (which will show up as an 404 error in the *Resources* panel)

Common gotchas:

* remember to rebuild and reload your extension after changing any config or code
* can't figure out the problem? Get in touch at support@trigger.io!

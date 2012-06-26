.. _forgeignore:

Excluding files from your builds
--------------------------------------------
To exclude files and folders in ``src`` from being included in the output of
``forge build``, you can write a set of exclusion rules in
``src/.forgeignore``. The following is an example ``.forgeignore`` file::

    ignoreme.txt
    *.swp
    ./tests/
    .git/
    ./identity.json

There are two types of exclusion rules: rules that check the *filename* of each
file and rules that check the *path* of each file (relative to the ``src``
directory).

*Excluding files based on their name*:
    Any rule without a / symbol in it is a filename rule. If you want to
    exclude any files called ``ignoreme.txt``, the correct pattern to use is
    just ``ignoreme.txt`` as shown above.

*Ignoring files with a specific extension*:
    Filename rules support glob syntax, so you can have rules that only
    consider part of the name. For example, ``*.swp`` will ignore
    ``index.html.swp`` and ``main.js.swp``.

*Ignoring all folders with a certain name (but not files)*:
    To exclude folders that match a rule but not files that match the rule,
    just add a trailing / symbol. E.g. ``.git/`` will exclude any folders
    called ``.git`` but include individual files with the same name.

*Ignoring a file at a specific path*:
    If you want to exclude a file at a particular location in your code, just
    specify the path to it. E.g. ``./identity.json`` will exclude
    ``identity.json`` at the top level of your ``src``, but any other files
    with that name will be included.

    Paths support globs too, so e.g. ``./temp/*.js`` will ignore all files
    matching ``*.js`` inside the temp folder.

.. note:: Windows users should make sure to always use / symbols as the folder separator (*forward slashes*) in your forgeignore file, these will ensure the exclusion rules work across different platforms

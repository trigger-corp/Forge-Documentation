.. _tools-hooks:

Using hooks
===========

To allow custom steps to be added to the Forge build process the Forge tools support hooks, which are scripts controlled by you which Forge will run at specific points in the build. These scripts are placed in the specific hook folder within a ``hooks`` folder in the top level of your app (next to ``src``). For example placing ``hook.py`` in ``hooks/prebuild`` would cause ``hook.py`` to be executed at the prebuild stage. Hooks are executed in alphabetical order.

Hooks types are defined by the file extension of the hook, the following hook types are currently supported:

- ``.py`` - Python hooks will be run by executing ``python hook.py``.
- ``.js`` - Node hooks will be run by executing ``node hook.js``.
- ``.sh`` - Shell hooks will be run by executing ``./hook.sh`` and will not work on Windows.
- ``.bat`` - Windows batch file hooks will be run by executing ``hook.bat`` and will only work on Windows.

Available hooks are:

- ``prebuild`` - The prebuild hook executes within the ``src`` directory before a build is run, however any changes will not affect the ``src`` directory contents after the build is finished, only the built apps. This allows preprocessing of files to occur.

Examples
~~~~~~~~

Below are a number of example hooks which can be pasted and either used as they are or as a starting point for creating your own.

coffeescript.js
---------------

.. code-block:: javascript

    // Compile all coffee files in the current tree to js and delete originals

    var cs = require("coffee-script");
    var fs = require("fs");

    files = fs.readdirSync('.');

    var processDir = function (dir) {
        fs.readdirSync(dir).forEach(function (file) {
            var stat = fs.statSync(dir+"/"+file);
            if (stat.isDirectory()) {
                processDir(dir+"/"+file);
            } else {
                var fileParts = file.split(".");
                if (fileParts[fileParts.length-1] == "coffee" && fileParts.length > 1) {
                    var script = fs.readFileSync(dir+"/"+file, "utf8");
                    fileParts[fileParts.length-1] = "js"
                    fs.writeFileSync(dir+"/"+fileParts.join("."), cs.compile(script), "utf8");
                    fs.unlinkSync(dir+"/"+file);
                    console.log("Compiled "+dir+"/"+file+" to "+dir+"/"+fileParts.join("."));
                }
            }
        });
    };

    processDir('.');

.. note:: Make you have installed the coffee-script module for node: ``npm install coffee-script``


less.js
-------

.. code-block:: javascript

    // Compile all less files in the current tree to css and delete originals

    var less = require("less");
    var fs = require("fs");

    files = fs.readdirSync('.');

    var processDir = function (dir) {
        fs.readdirSync(dir).forEach(function (file) {
            var stat = fs.statSync(dir+"/"+file);
            if (stat.isDirectory()) {
                processDir(dir+"/"+file);
            } else {
                var fileParts = file.split(".");
                if (fileParts[fileParts.length-1] == "less" && fileParts.length > 1) {
                    var script = fs.readFileSync(dir+"/"+file, "utf8");
                    fileParts[fileParts.length-1] = "css"
                    fs.unlinkSync(dir+"/"+file);
                    less.render(script, function (e, css) {
                        fs.writeFileSync(dir+"/"+fileParts.join("."), css, "utf8");
                        console.log("Compiled "+dir+"/"+file+" to "+dir+"/"+fileParts.join("."));
                    });
                }
            }
        });
    };

    processDir('.');

.. note:: Make you have installed the less module for node: ``npm install less``
.. _modules-activations:

``activations``: Inject files into pages
================================================================================

**Platforms: Browser**

The ``activations`` module allows styles and scripts to be injected into webpages with specified URLs.

Config
------

The ``activations`` module must be enabled in config.json as follows:

.. parsed-literal::
    {
        "modules": {
            "activations": [
                {
                    ":ref:`patterns <field-activations-patterns>`": ["http://mail.google.com"],
                    ":ref:`scripts <field-activations-scripts>`": ["gmail.js"],
                    ":ref:`styles <field-activations-styles>`": ["gmail.css"],
                    ":ref:`run_at <field-activations-runat>`": "start",
                    ":ref:`all_frames <field-activations-allframes>`": false
                }
            ]
        }
    }
    
This field specifies when and how your foreground files will be embedded into pages. 
It is an array of objects with three required keys:

.. _field-activations-patterns:

.. _field-activations-scripts:

.. _field-activations-styles:


* ``patterns`` is an array of `Match Patterns <http://code.google.com/chrome/extensions/match_patterns.html>`_ which control on which URLs your app will activate
* ``scripts`` is an array of Javascript files which will be embedded
* ``styles`` is an array of CSS files which will be embedded

As well as an optional keys:

.. _field-activations-runat:

* ``run_at`` optionally defines when your included scripts will be added to the page, must be one of the following:

 * ``"start"`` scripts will be run immediately, potentially before the DOM is ready
 * ``"ready"`` scripts will run as soon as the DOM is ready
 * ``"end"`` (default) scripts will run at some point after the DOM is ready, with no guarantees as to whether or not ``window.onload`` will have fired yet or not.

.. _field-activations-allframes:

* ``all_frames`` optionally defines whether activations will be run in all frames or just the top level document, by default it is false.

.. important:: Safari only supports a single object in the activations array.

.. _field-browser_action:
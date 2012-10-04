How to generate the documentation
============================================

First, create a virtual Python environment::

    virtualenv documentation
    cd documentation
    source bin/activate

Then grab this documentation::

    hg clone ssh://hg@bitbucket.org/webmynd/forge-documentation .

Then install the requirements::

    pip install -r requirements.txt

Then generate the docs::

    sphinx-build -a -b html source/ build/

Open ``build/index.html`` to see the results!

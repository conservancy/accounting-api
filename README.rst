.. vim: textwidth=80

=======================
 accounting-api README
=======================

--------------
 Dependencies
--------------

-   Python >=3.3
-   ledger version 3 (I have not tried with version 2.x)
-   Python packages: Flask, etc. (install by running ``pip install -r
    requirements.txt``)

~~~~~~~~~~~~~~~~~~~~~~~~~
 GTK Client Dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~

To run the GTK client you need to have ``gi.repository`` avaiable in the python
environment, this means that if you use virtualenv to install the dependencies
of accounting-api you need to set it up with the ``--system-site-packages``
flag.

---------------------------------------
 Installation (i.e. Development Setup)
---------------------------------------

accounting-api does not yet have a method for end-user installation. This
section describes how you would set up accounting-api for development purposes,
which can also be used as an environment to try out the functionality of
accounting-api.

See the sections below on how to install the dependencies. Then run the
following in your shell.

.. code-block:: bash

    # Get the source code
    git clone git://gitorious.org/conservancy/accounting-api.git
    cd accounting-api

    # Set up the python 3.3 virtualenv (this will make the GTK client not work)
    mkvirtualenv -p /usr/bin/python3.3 accounting-api
    # OR If you want the GTK client to work
    mkvirtualenv -p /usr/bin/python3.3 --system-site-packages accounting-api

    # If your terminal prompt does not say "(accounting-api)", run
    workon accounting-api

    # Install the python packages
    pip-3.3 install -r requirements.txt

If all went well, head to :ref:`usage`. If not, head to the channel ``#npoacct``
on ``irc.freenode.net``.

~~~~~~~~
 Ubuntu
~~~~~~~~


.. code-block:: bash

    # git python 3.3 and virtualenvwrapper
    sudo apt-get install git-core python3.3 virtualenvwrapper

    # ledger 3
    sudo apt-add-repository ppa:mbudde/ledger
    sudo apt-get update
    sudo apt-get install ledger

~~~~~~~~~~~~~
Debian wheezy
~~~~~~~~~~~~~

.. code-block:: bash

    # git python 3.3, virtualenvwrapper, sphinx (and related modules)
    sudo aptitude install git-core python3.3 virtualenvwrapper sphinx python-sphinxcontrib-httpdomain python-flask python-flaskext.wtf  python3-sqlalchemy python-sqlalchemy-doc

    # ledger 3
    # Build this from upstream sources

.. _usage:

-------
 Usage
-------

.. code-block:: bash

    # Run the web service
    LEDGER_FILE=../path/to/your.ledger ./bin/serve

    # Get a balance report via the web service
    ./bin/client balance

    # Get the transaction log
    ./bin/client register

    # Insert a simple transaction, currency will be autodetected from your
    # locale, for another currency, use ``--symbol USD``
    ./bin/client insert "January rent" Assets:Checking Expenses:Rent 654.32

============
Installation
============

Git
---

1. Clone and change to the directory::

    $ git clone https://opendev.org/openstack/openstack-tempest-skiplist
    $ cd openstack-tempest-skiplist

2. Create a virtual environment using :command:`virtualenv`::

    $ virtualenv .venv
    $ source .venv/bin/activate

3. Install requirements in the newly created virtual environment::

    (.venv) $ pip install .

4. *(optional)* Instead of manual installation described in steps 2 and 3
   above, tox can be used for installing the requirements as well.
   To create python 3.6 environment run following::

    $ tox -epy36
    $ source .tox/py36/bin/activate

Pip installation
----------------

Install ``openstack-tempest-skiplist`` via pip as follows::

   $ pip install openstack-tempest-skiplist

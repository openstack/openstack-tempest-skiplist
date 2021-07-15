openstack-tempest-skiplist
==========================

Overview
--------

openstack-tempest-skiplist will generate a skip list to be executed by tempest

-  Free software: Apache license
-  Documentation: https://docs.openstack.org/openstack-tempest-skiplist/latest/
-  Source: https://opendev.org/openstack/openstack-tempest-skiplist
-  Bugs: https://storyboard.openstack.org/#!/project/1173
-  Release notes: https://docs.openstack.org/releasenotes/openstack-tempest-skiplist

Quickstart
==========

- edit tempest_skip.yml
- add the required fields, including the launchpad
- execute tox tests
- submit :)

Installation
------------

Installing from git and virtualenv::

    $ git clone https://opendev.org/openstack/openstack-tempest-skiplist
    $ cd openstack-tempest-skiplist
    $ virtualenv .venv
    $ source .venv/bin/activate
    $ pip install .

Validation
----------

After edit your file, you can check if it is valid with the following command::

    $ tempest-skip validate --file file.yaml

Examples
--------

A simple example of the structure of the yaml file expected by
tempest-skiplist.
For more information about each field, visit the `documentation <https://docs.openstack.org/openstack-tempest-skiplist/latest/yaml/formatting.html>` website:

.. code-block:: yaml

    known_failures:
    - test: 'full.tempest.test'
        bz: 'https://bugzilla.redhat.com/1'
        lp: 'https://launchpad.net/bugs/1'
        deployment:
          - 'undercloud'
          - 'overcloud'
        jobs:
          - job1
          - job2
        reason: 'default reason'
        releases:
          - name: master
            lp: 'https://launchpad.net/bugs/2'
            reason: 'Some reason'
          - name: train
            bz: 'https://bugzilla.redhat.com/train1'
            installers:
              - 'osp'
          - name: ussuri
            installers:
              - 'tripleo'
            bz: 'https://bugzilla.redhat.com/ussuri1'

In the above example, the test *full.tempest.test* will be executed by tempest
in both deployments, undercloud, and overcloud (depending on the job).
It will also be skipped in the releases master, train and ussuri, specifically
in jobs job1 and job2. It will not be skipped in any other job, no matter what
the release is.

Removing the list of jobs, means it will be skipped everywhere.

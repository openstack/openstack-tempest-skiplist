==========
Formatting
==========

YAML File
---------

The YAML file used by `openstack-tempest-skiplist` use the following pattern:

.. code-block:: yaml

    - test: 'full.tempest.test'
      bz: 'bugzilla bug'
      lp: 'launchpad bug'
      deployment: 'undercloud or overcloud'
      jobs:
        - job1
        - job2
      releases:
        - master
          lp: 'master launchpad'
        - train
          bz: 'train bugzilla'
        - ussuri


YAML values
-----------


LP and BZ
+++++++++

One of them is required, not both, but it's crucial that people are able to
trackdown the reason the test is being added in the skiplist.
Here there are two levels of lp and bz: the first one, is the global lp and bz
and the second is based on the release. This is required because it's possible
to have the test failing in two different releases but with different reasons.
If the lp or bz is set on test level, you don't need to add it per release, it
will use the test level.


Releases
++++++++

Releases contain a list of releases that the test will be skipped. It's very
common that in a release the test is passing, but in another don't, so we can
manage it here.


Jobs
++++

This is a list of jobs where the test should be skipped. This is not a
required field, however, once set, the tool will return the test only if the
job matches.


Deployment
++++++++++

This is right now TripleO only configuration, since it deploys two different
openstack instances, undercloud and overcloud. Default to overcloud
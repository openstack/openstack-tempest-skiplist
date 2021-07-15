==========
Formatting
==========

YAML File
---------

The YAML file used by `openstack-tempest-skiplist` use the following pattern:

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
        - name: ussuri
          bz: 'https://bugzilla.redhat.com/ussuri1'


YAML values
-----------


BZ and LP
+++++++++

One of them is required, not both, but it's crucial that people are able to
trackdown the reason the test is being added in the skiplist.
Here there are two levels of lp and bz: the first one, is the global lp and bz
and the second is based on the release. This is required because it's possible
to have the test failing in two different releases but with different reasons.
If the lp or bz is set on test level, you don't need to add it per release, it
will use the test level.
The value of both lp and bz are their respective URL


Deployment
++++++++++

This is right now TripleO only configuration, since it deploys two different
openstack instances, undercloud and overcloud. Default to overcloud.


Installers
++++++++++
This is a list of installers per release where the test will be
skipped. The options for installers are 'tripleo' and 'osp',
where 'tripleo' is the upstream installer and 'osp' is the
downstream installer.
The default (if this option is not set) is 'tripleo' and 'osp'.


Jobs
++++

This is a list of jobs where the test should be skipped. This is not a
required field, however, once set, the tool will return the test only if the
job matches.


Reason
++++++

This is a description about why this test is being skipped. It exists in two
levels, the first in the test level, that will be the default reason, and in
release level, where reason can be different.


Releases
++++++++

Releases contain a list of releases that the test will be skipped. It's very
common that in a release the test is passing, but in another don't, so we can
manage it here.
Here, it's also required a reason, and a lp or a bz

Examples
--------

Below are some examples of valid yaml files that can be used:

No releases
+++++++++++

Since there's no releases, this will be valid for all releases:

.. code-block:: yaml

  known_failures:
    - test: 'tempest_skip.tests.test_validate'
      bz: 'https://bugzilla.redhat.com/1'
      lp: 'https://launchpad.net/bugs/1'
      deployment:
        - 'undercloud'
      reason: 'This test will be skipped in any release'


With releases
+++++++++++++

As release is set, the test will be skipped only on the matching releases

.. code-block:: yaml

  known_failures:
    - test: 'tempest_skip.tests.test_validate'
      bz: 'https://bugzilla.redhat.com/1'
      lp: 'https://launchpad.net/bugs/1'
      deployment:
        - 'undercloud'
      reason: 'This test will be skipped in any release'
      releases:
        - name: rocky
          reason: 'Test failing in rock because of network'
          lp: 'https://launchpad.net/bugs/1'
        - name: ussuri
          reason: 'Test is failing in ussuri because of storage bug'
          bz: 'https://bugzilla.redhat.com/1'


With jobs
+++++++++

If a list of jobs is set, the test will be skipped only in the matching jobs

.. code-block:: yaml

  known_failures:
    - test: 'tempest_skip.tests.test_validate'
      bz: 'https://bugzilla.redhat.com/1'
      lp: 'https://launchpad.net/bugs/1'
      deployment:
        - 'undercloud'
      reason: 'This test will be skipped in any release'
      jobs:
        - tempest-test-job-skip1
        - tempest-test-job-skip2


With jobs and releases
++++++++++++++++++++++

This test will be skipped only when it matches both, job and release

.. code-block:: yaml

  known_failures:
    - test: 'tempest_skip.tests.test_validate'
      bz: 'https://bugzilla.redhat.com/1'
      lp: 'https://launchpad.net/bugs/1'
      deployment:
        - 'undercloud'
      reason: 'This test will be skipped in all releases'
      releases:
        - name: rocky
          reason: 'Test failing in rock because of network'
          lp: 'https://launchpad.net/bugs/1'
        - name: ussuri
          reason: 'Test is failing in ussuri because of storage bug'
          bz: 'https://bugzilla.redhat.com/1'
      jobs:
        - tempest-test-job-skip1
        - tempest-test-job-skip2


With releases and installers
++++++++++++++++++++++++++++

.. code-block:: yaml

  known_failures:
    - test: 'tempest_skip.tests.test_validate'
      bz: 'https://bugzilla.redhat.com/1'
      lp: 'https://launchpad.net/bugs/1'
      deployment:
        - 'overcloud'
      reason: 'This test will be skipped in any release'
      releases:
        - name: train
          reason: 'Test failing in train because of network'
          installers:
            - 'tripleo'
          lp: 'https://launchpad.net/bugs/1'
        - name: wallaby
          reason: 'Test is failing in /osp-17 because of storage bug'
          installers:
            - 'osp'
          bz: 'https://bugzilla.redhat.com/1'

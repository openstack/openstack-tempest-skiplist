==================
List allowed tests
==================

List allowed tests
------------------

You can use :command:`tempest-skip list-allowed` command to list the tests to
be executed with two positional parameters which are in the
expected format::

    1. ``--file`` is the positional parameter - list all the tests in the file
    2. ``--group`` or ``--job`` - filter the tests for a specific job, or a
           specific group.

Job filter
----------

The job filter, is as the name indicate, it checks the yaml file for a job that
matches (must be full match, not partial), and list the tests related to that
specific job::

    $ tempets-skip list-allowed --file tempest_allow.yml --job job1

Group filter
------------

The group filter, which have precedence on the ``--job``, will list the tests
for a particular group. This is good when you have several jobs, that run a
specific set of tests. In this case, you don't need to repeat the same set of
tests for several different jobs::

    $ tempest-skip list-allowed --file tempest_allow.yml --group default_group

Release filter
--------------

The release filter, which is default to master, filter based on group or job
for an specific release.

Multiple Groups with same name
------------------------------------------

Multiple groups can have same name with different tests and releases. This
behaviour allows us to classify the tests on the basis of releases. Here, we
cannot define a release more than once in such groups i.e groups having same
name should mandatorily have different releases::

  - name: featureset062  # standalone-jobs
    tests:
      - 'octavia_tempest_plugin.tests.scenario.v2.test_healthmonitor'
      - 'octavia_tempest_plugin.tests.scenario.v2.test_listener'
    releases:
      - master
      - wallaby
  - name: featureset062  # standalone-jobs
    tests:
      - 'octavia_tempest_plugin.tests.scenario.v2.test_healthmonitor'
      - 'octavia_tempest_plugin.tests.scenario.v2.test_l7policy'
    releases:
      - train

Wildcard filter for releases
----------------------------

If in the releases list in the yaml file, the release ``all`` is set, that
means, it will not matter which release is passed to ``tempest-skip`` command,
it will be included in the final list.

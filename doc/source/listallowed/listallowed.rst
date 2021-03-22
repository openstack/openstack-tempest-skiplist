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

======================
List skipped tests
======================

List skipped tests
-------------------

You can use :command:`tempest-skip list-skipped` command to list tests in the yaml
file with one positional and two optional parameters which is in the expected
format::

    1. ``--file`` is the positional parameter - lists all the tests in the file::

        $ tempest-skip list-skipped yaml --file tempest_skip.yml

    2. ``--release``, ``--deployment``, ``--installer`` and  ``--job`` are the
       optional parameters - list all the tests within a specific release,
       deployment or a specific job::

       $ tempest-skip list-skipped --file tempest_skip.yml --release train
       $ tempest-skip list-skipped --file tempest_skip.yml --job job1
       $ tempest-skip list-skipped --file tempest_skip.yml --release train --job job1
       $ tempest-skip list-skipped --file tempest_skip.yml --deployment undercloud
       $ tempest-skip list-skipped --file tempest_skip.yml --installer tripleo

This will return any tests that match the job, as well as tests that doesn't
have any job configured. This is required when you configure your zuul jobs to
always parse the ``--job`` option. In this scenario, if a job2 is parsed, and
there is no test with job2, it would return zero tests to be skipped, which is
not the intent. The test with no job defined, means, skip everywhere, if you
define the job in the test yaml file, it means, skip all the tests that doesn't
have a job defined, plus this test.

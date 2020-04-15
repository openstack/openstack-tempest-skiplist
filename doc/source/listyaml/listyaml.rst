======================
List the yaml file
======================

List Yaml
----------

You can use :command:`tempest-skip` list command to list tests in the yaml
file with one positional and two optional parameters which is in the expected
format::

1. ``--file`` is the positional parameter - lists all the tests in the file::

    $ tempest-skip list yaml --file tempest_skip.yml

2. ``--release`` and job are the optional parameters - list all the tests
   within specific release or specific job::

   $ tempest-skip list yaml --file tempest_skip.yml --release train
   $ tempest-skip list yaml --file tempest_skip.yml --job job1
   $ tempest-skip list yaml --file tempest_skip.yml --release train --job job1


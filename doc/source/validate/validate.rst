======================
Validate the yaml file
======================

Validation
----------

You can use :command:`tempest-skip` validate command to validate if the yaml
file is in the expected format::

    $ tempest-skip validate --file good_file.yaml


This will return nothing if the file is valid, or an error otherwise::

    $ tempest-skip validate --file bad_file.yaml
    required key not provided @ data['known_failures'][0]['releases'][2]['reason']
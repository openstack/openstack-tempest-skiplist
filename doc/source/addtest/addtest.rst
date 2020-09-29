========================
Adding tests to skiplist
========================

Adding tests
------------

Of course it is possible to directly edit the yaml file and add the test
itself, but that may lead to failures, as for example duplicated entries,
identation issues, having a namespace test instead of full path test name.

In order to avoid that, you can use the `addtest` command that will identify if
the test is already on the skiplist, avoiding duplication. It will also
generate the yaml file properly as well as avoid the use of test namespace. For
example, if a user tries to add the tempest.scenario, it will skip all the
tests under tempest.scenario, which is not the desirable behavior. However, it
is a lot of work to add each entry under tempest.scenario, since we must repeat
all the reasons, bugzilla, releases, etc.

The addtest command solves all these problems for you. First of all, when you
try to add a test passing a test namespace, addtest will give you a list of
tests under that particular namespace, where you can choose from the list which
ones you would like to add. Select the ones you want and you are done!

Examples
--------

The command below add the test tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_connectivity_between_vms_on_different_networks::

    $ tempest-skip addtest \
                   --file roles/validate-tempest/vars/tempest_skip.yml \
                   --release master \
                   --test tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_connectivity_between_vms_on_different_networks \
                   --reason 'Failing on network' \
                   --lp https://launchpad.net/bug/12345

In this example, we are adding the full path test, and so, the command will not
prompt you a list of tests that you want to choose. If for example, only the
namespace be parsed, you will be prompted with a list of tests under that
namespace::

    $ tempest-skip addtest \
                   --file roles/validate-tempest/vars/tempest_skip.yml \
                   --release master \
                   --test tempest.scenario.test_network_basic_ops \
                   --reason 'Failing on network' \
                   --lp https://launchpad.net/bug/12345

And this is the output:

.. code-block::

    [?] These are the tests available on the namespace, choose which ones you want to add. Press space to select:
     > o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_connectivity_between_vms_on_different_networks
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_hotplug_nic
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_mtu_sized_frames
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_network_basic_ops
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_port_security_macspoofing_port
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_preserve_preexisting_port
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_router_rescheduling
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_subnet_details
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_update_instance_port_admin_state
       o tempest.scenario.test_network_basic_ops.TestNetworkBasicOps.test_update_router_admin_state

You can use the arrow keys on your keyboard to navigate through the list, and
space to select. Once you are done, just press enter, the command will go
through each test, check if the test exists or not. If it exists, it will also
check the release exists, and properly add the test.

Once you are done, you can validate if the yaml file was generated properly
with the command::

    $ tempest-skip validate --file roles/validate-tempest/vars/tempest_skip.yml

There are some arguments you can pass to the addtest, the required ones are:

* --file
* --lp or --bz
* --reason

All the other arguments have default values, for example, `--release` default
value is master and `--deployment` default value is overcloud

For more information, use::

    $ tempest-skip addtest --help

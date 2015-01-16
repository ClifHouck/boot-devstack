# boot-devstack #
A simple 
<a href="https://en.wikipedia.org/wiki/Ansible_(software)">ansible</a> 
playbook to provision and boot a single
<a href="http://docs.openstack.org/developer/devstack/">Devstack</a> 
(see <a href="http://www.openstack.org/">OpenStack</a>) instance
using the Rackspace cloud. 

## Examples #
All examples assume execution from the repository root.

    $ ansible-playbook boot-devstack.yml

to boot a machine using the default options. 

    $ ansible-playbook boot-devstack.yml -e "devstack_config_filename=ironic-pxe-driver-local.conf"

boots a devstack instance using a version of local.conf which uses enables the 
PXE driver for use under Ironic.

## Notes #
You must have ansible and pyrax installed and configured to use this playbook.

Currently, this repo contains two 
<a href="https://wiki.openstack.org/wiki/Ironic">Ironic</a>-specific devstack
configurations taken from the Ironic 
<a href="http://docs.openstack.org/developer/ironic/dev/dev-quickstart.html">developer quickstart guide</a>.

You can select the devstack configuration you want by over-riding the 
'devstack_config_filename' variable. Available configurations are found in
the ${repository_root}/roles/devstack/files/ directory.

Also, there's a task file in ${repo_root}/roles/devstack/tasks/customization_tasks.yml
where you can specify custom tasks you want to execute before ./stack.sh is run.

You will likely want to change the name of the key-pair you use in
${repo_root}/roles/localhost/vars/main.yml, since I hope you're not using mine!

Needs work to make it more flexible and useful! Feel free to contribute!

# boot-devstack
A simple 
<a href="https://en.wikipedia.org/wiki/Ansible_(software)">ansible</a> 
playbook to provision and boot a single
<a href="http://docs.openstack.org/developer/devstack/">Devstack</a> 
(see <a href="http://www.openstack.org/">OpenStack</a>) instance
using the Rackspace cloud. 

## Requirements
You must have ansible and pyrax installed and configured to use this playbook.

You will likely want an entry for localhost in your /etc/ansible/hosts file. Like so:

    [localhost]
    localhost ansible_connection=local

## Important Playbook Variables

You probably want to change one or more of these playbook variables to suit
your needs.

* <b>key_name</b>: The ssh key-pair name to inject to the devstack host.
* <b>server_name</b>: What to name the new devstack server.
* <b>flavor</b>: The type of machine to spool for the devstack server.
* <b>image</b>: The OS image to use on the devstack server.
* <b>environment</b>: The pyrax environment to use when requesting a new server.
* <b>devstack_config_filename</b>: The file to use as devstack's local.conf. 
Available configurations are located in the devstack 
<a href="https://github.com/ClifHouck/boot-devstack/tree/master/roles/devstack/files">files</a>
folder

## Examples
All examples assume execution from the repository root.

    $ ansible-playbook boot-devstack.yml

to boot a machine using the default options. 

    $ ansible-playbook boot-devstack.yml -e "devstack_config_filename=ironic-pxe-driver-local.conf"

boots a devstack instance using a version of local.conf which uses enables the 
PXE driver for use under Ironic.

## Devstack Configuration
Currently, this repo contains two 
<a href="https://wiki.openstack.org/wiki/Ironic">Ironic</a>-specific devstack
configurations taken from the Ironic 
<a href="http://docs.openstack.org/developer/ironic/dev/dev-quickstart.html">developer quickstart guide</a>.

You can select the devstack configuration you want by over-riding the 
'devstack_config_filename' variable. Available configurations are found in
the ${repository_root}/roles/devstack/files/ directory.

Also, there's a task file in ${repo_root}/roles/devstack/tasks/customization_tasks.yml
where you can specify custom tasks you want to execute before ./stack.sh is run.

## Notes

You will likely want to change the name of the key-pair you use in
${repo_root}/roles/localhost/vars/main.yml, since I hope you're not using mine!

Needs work to make it more flexible and useful! Feel free to contribute!

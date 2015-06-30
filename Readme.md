OpenShift Kickstarter
=====================

I have created this repository to reduce the time necessary to install OpenShift v3 for Demos and PoC's

## Files

- `ansible_inventory` - this file holds the information about your desired environment.
- `openshift_prereqs.yml` - is a Ansible Playbook to make sure your systems are able to talk to each other and that fulfills the necessary prerequisites.
- `openshift_aws and openshift_aws.pub` - These are the ssh key files that are used to login from the master to the nodes.
- `installer.cfg.yml` - is the installer configuration file
- `example_hosts` - is the example hosts file, that is used to prepare the ansible installation from the master.

## Next Steps

Review ansible_inventory and make sure the content matches your environment. In the default case I have set it up in the following way:

```
[openshift_nodes]
openshift-master.openshift.me
openshift-node1.openshift.me
openshift-node2.openshift.me

[openshift_master]
openshift-master.openshift.me
```

which means that I will have one master and 2 nodes. Plus I will let the master act as a node as well.

### Environment Variables

Make sure to create a file or create the environment variables by hand

```
export RHN_USER=<your RHN username>
export RHN_PASS=<your RHN Password>
export ANSIBLE_USER=<username used to connect to remote systems>
export ANSIBLE_SUDO=<Whether the user should use sudo>
```

you can use the `env.example` file for your convenience to prepare your environment.

```
mv env.example env
vi env # edit the file and add the appropriate values
source env
```

to run the installer run the following command:

```
ansible-playbook -i ./ansible-inventory ./openshift_prereqs.yml
```

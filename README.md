# eap-httpd-lb-demo

Demonstration of a JBoss EAP servers load balanced using HTTPD

## Prerequisites

### Download dependencies

Execute the following commands to download the required dependencies

```
$ ansible-galaxy collection install -r collections/requirements.yml
```

```
$ ansible-galaxy role install -r collections/requirements.yml
```

### Populate Inventory

Add the HTTPD and EAP instances into the [hosts](inventory/hosts) file.

### Subscription Information

The content within this repository leverages Red Hat RPM's. The automation to manage subscribing the machines and repositories makes use of the [rhsm](https://github.com/redhat-cop/infra-ansible/blob/master/roles/rhsm) role within the [infra-ansible](https://github.com/redhat-cop/infra-ansible) repository.

It is recommended to add the necessary values to a separate file and inject it in as an extra parameter using `-e @<filename>` when executing the playbook

## Provision

Provision the environment by executing the following command:

```
$ ansible-playbook -i inventory/  playbooks/demo.yml
```

### Mod Cluster Manger

The Mod Cluster Manager application allows for viewing the state of the load balanced EAP instances within the HTTPD server. By default, this application is not exposed. It can be exposed at the `/mod_cluster_manager` context path of HTTTD by specifying `-e mod_cluster_expose=true` when provisioning the environment.

## Development Notes

The contents in this repository leverage assets from unreleased artifacts. In particular, you must have the most recent [jcliff](https://github.com/wildfly-extras/ansible_collections_jcliff) available.

Execute the following steps to prepare your environment

```
$ mkdir -p collections/ansible_collections/wildfly
$ pushd collections/ansible_collections/wildfly
$ git clone https://github.com/wildfly-extras/ansible_collections_jcliff jcliff
$ popd
```

_NOTE:_ You should remove the collection that may have been installed during the prerequisites section prior to cloning the upstream repository
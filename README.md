This repository directory contains Heat templates to deploy under-cloud environment for ONAP Beijing.
It:
- creates Rancher server
- creates defined number of Kubernetes Nodes
- configures Rancher Server and adds Rancher Agents on each Kubernetes Nodes
- sets up NFS cluster
- configures kubectl and Helm repository on Rancher Server

### Usage ###

**Note!** You need to use OpenStack CLI, because this project contains nested Heat templates that are not applicable to Horizon UI.

First you need to install and configure Heat client (http://docs.openstack.org/user-guide/common/cli-install-openstack-command-line-clients.html):

```
apt-get install python-dev python-pip
pip install python-heatclient        # Install heat client
pip install python-openstackclient   # Install the Openstack client to support multiple services
```

Create a file with OpenStack credentials (e.g. openrc):

```
export OS_AUTH_URL=INSERT THE AUTH URL HERE
export OS_USERNAME=INSERT YOUR USERNAME HERE
export OS_TENANT_ID=INSERT YOUR TENANT ID HERE
export OS_REGION_NAME=INSERT THE REGION HERE
export OS_PASSWORD=INSERT YOUR PASSWORD HERE
```

Export variables:

`source openrc`


Enter heat/ directory and edit environment file. Example below:

```
ubuntu_1604_image: Ubuntu 16.04 LTS (Xenial Xerus) [20180126]
rancher_vm_flavor: m1.small
k8s_vm_flavor: m1.small
key_name: onap-dev
k8s_node_count: 1
```

Create Heat stack:

`openstack stack create -t onap-cloud.yaml -e onap-cloud.env ONAP`

It should install a new Heat stack with VMs ready to deploy ONAP via OOM.
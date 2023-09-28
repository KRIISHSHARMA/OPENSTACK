# INSTALLING OPENSTACK
### In order to install OpenStack, execute the following command:
``` bash
sudo snap install openstack --edge
```
### In order to install all necessary dependencies, execute the following command:
``` bash
sunbeam prepare-node-script | bash -x && newgrp snap_daemon
```
### In order to bootstrap the cloud, execute the following command:
```bash
sunbeam cluster bootstrap --accept-defaults
```
### In order to configure the cloud with default options, execute the following command:
```bash
sunbeam configure --accept-defaults --openrc demo-openrc
```

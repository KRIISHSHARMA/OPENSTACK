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

# LAUNCHING AN INSTANCE 
### In order to launch your first instance, execute the following command:
```bash
sunbeam launch ubuntu --name test
```
### output:
/// Access instance with `ssh -i /home/ubuntu/.config/openstack/sunbeam ubuntu@10.20.20.16`
### At this point the instance should be accessible over the SSH protocol. In order to connect to it, execute the command from the output:
```bash
ssh -i /home/ubuntu/.config/openstack/sunbeam ubuntu@10.20.20.16
```


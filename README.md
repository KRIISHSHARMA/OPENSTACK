# INSTALLING OPENSTACK(using devstack)
### WHAT IS OPENSTACK 
- OpenStack is a free, open standard cloud computing platform. It is mostly deployed as infrastructure-as-a-service in both public and private clouds where virtual servers and other resources are made available to users
## Step 1: Update and Upgrade the System
```bash
apt update -y && apt upgrade -y
```
## Step 2: Create Stack user and assign sudo priviledge
```bash
sudo useradd -s /bin/bash -d /opt/stack -m stack
```
```bash
sudo chmod +x /opt/stack
```
### Next, run the command below to assign sudo privileges to the user
```bash
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
```
## Step 3: Install git and download DevStack
```bash
su - stack
```
### Once you have successfully created the user ‘stack’ and assigned sudo privileges, switch to the user using the command.
```bash
sudo apt install git -y
```
### Using git, clone devstack’s git repository as shown.
```bash
git clone https://git.openstack.org/openstack-dev/devstack
```
## Step 4: Create devstack configuration file
### In this step, navigate to the devstack directory.
```bash
cd devstack
```
### Then create a local.conf configuration file.
```bash
vim local.conf
```
### Paste the following content
```bash
[[local|localrc]]
# Password for KeyStone, Database, RabbitMQ and Service
ADMIN_PASSWORD=StrongAdminSecret
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
# Host IP - get your Server/VM IP address from ip addr command
HOST_IP=10.208.0.10
```
#### Save and exit the text editor. NOTE:

The ADMIN_PASSWORD is the password that you will use to log in to the OpenStack login page. The default username is admin.
The HOST_IP is your system’s IP address that is obtained by running ifconfig or ip addr commands.
## Step 5: Install OpenStack with Devstack
### To commence the installation of OpenStack on Ubuntu 22.04, run the script below contained in devstack directory.
```bash
./stack.sh
```
#### The following features will be installed:

Horizon — OpenStack Dashboard
Nova — Compute Service
Glance — Image Service
Neutron — Network Service
Keystone — Identity Service
Cinder — Block Storage Service
Placement — Placement API
The deployment takes about 10 to 15 minutes depending on the speed of your system and internet connection. In our case, it took roughly 12 minutes. At the very end, you should see output similar to what we have below.

## Step 6: Accessing OpenStack on a web browser
#### To access OpenStack via a web browser browse your Ubuntu’s IP address as shown. https://server-ip/dashboard This directs you to a login page as shown.


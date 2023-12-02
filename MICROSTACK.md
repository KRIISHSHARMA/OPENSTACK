## Deploying openstack on a single node using microstack
- MicroStack is an Ubuntu solution for the installation of OpenStack on a single machine.
- MicroStack was designed for small-scale cloud environments, edge deployments, testing, and development.
- Cloud computing systems like OpenStack, can be complex due to their need to manage many interconnected resources and require certain technical skills to deploy in production.
-  Microstack can be a good stepping stone and starting point. MicroStack is opinionated and not as configurable to help reduce some of the complexity.
- Resources for installation
  1. [video source](https://www.youtube.com/watch?v=kuhEtsknpn4)
  2. [text resource](https://ubuntu.com/tutorials/install-openstack-on-your-workstation-and-launch-your-first-instance#1-overview)
  3. [microstack tutorial](https://ubuntu.com/openstack/tutorials)
- my network is 172.31.80.0/20 (ip route list)
  - gateway is 172.31.80.1
  - static ips from .10 to .19 for metallb (exposing OS controlplane)
  - static ips from .20 to .59 for openstack(routers etc)
1. Install microk8s
   ``` bash
   sudo snap install microk8s --channel 1.25-strict/stable
   ```
2. after microk8s installs its still running some tasks in the background to finish the config , to wait for those tasks to finish before moving to next step
   ``` bash
   sudo microk8s status --wait-ready
   ```
3. pointing to a public dns server
   ``` bash
   sudo microk8s enable dns:8.8.8.8,8.8.4.4
   ```
4. enabling hostpath-storage module
   ``` bash
   sudo microk8s enable hostpath-storage
   ```
5. enable and config ip range for metallb module
   ``` bash
   sudo microk8s enable metallb 172.31.80.10-172.31.80.19
   ```
6. add youself to snap microk8s root
   ``` bash
   sudo touch /var/snap/microk8s/current/var/lock/no-cert-reissue
   ```
7. add yourself to microk8s group
   ``` bash
   sudo usermod -a  -G snap_microk8s $USER
   ```
![Screenshot from 2023-12-02 10-03-30](https://github.com/KRIISHSHARMA/OPENSTACK/assets/86760658/5887b9aa-c91d-4920-8929-393953be4553)

- As you can see its not active yet so exit vm and log back in
![Screenshot from 2023-12-02 10-04-55](https://github.com/KRIISHSHARMA/OPENSTACK/assets/86760658/22417f2c-abe8-446c-830d-029957a2e88e)

8. installing juju
   ``` bash
    sudo snap install juju --channel 3.1/stable
   ```
9. install microstack from sunbeam channel
    ``` bash
    sudo snap install microstack --channel sunbeam/beta
    ```
10. installing openstack hypervisor packages which have pieces that will be running outside k8s
    ``` bash
    sudo snap install openstack-hypervisor --channel xena/beta
    ```
11. installing openstackclients
    ``` bash
    sudo snap install openstackclients --channel xena/beta
    ```
12. will need an ssh key to use to enter the vms so will create one rn
    ``` bash
    ssh-keygen -t rsa -q -f "$HOME/.ssh/id_rsa" -N ""
    ```
13. bootstraping
    ``` bash
    microstack bootstrap
    ``` 
15. to see the ineraction between juju and k8s while bootstraping
    ``` bash
    watch --color -- juju status --color -m openstack
    ```
    ``` bash
    watch microk8s.kubectl get all -A
    ```
    

# Netdata streaming implementation using ansible and vagrant
This reposiroty creates a simple scenario of using netdata stream
## Prerequisites
In order to run this scenario you need three things installed on your system:
1. [Ansible](https://www.ansible.com/)
2. [Vagrant](https://www.vagrantup.com/)
3. [VirtualBox](https://www.virtualbox.org/)
## How to run
Running this project is as simple as cloning the project and running the following command in the terminal:
```
vagrant up
```
After deployment, you can access the grafana dashboard using this URL:
```
http://<netdata_master>:19999
```
Where `netdata_master` is IP address of your master netdata node.

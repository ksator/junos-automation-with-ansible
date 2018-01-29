[![Build Status](https://travis-ci.org/ksator/ansible-training-for-junos-automation.svg?branch=master)](https://travis-ci.org/ksator/ansible-training-for-junos-automation)

# About this project   
This project has many ready-to-use Ansible playbooks to interact with Junos devices.    

# About Ansible

[Here's an ansible presentation](ansible.pdf)  

[Ansible vs Saltstack vs Stackstorm](https://medium.com/@anthonypjshaw/ansible-v-s-salt-saltstack-v-s-stackstorm-3d8f57149368)  

# Ansible modules for Junos automation

There are two modules librairies to interact with Junos
- An Ansible library for Junos built by Juniper
    - These modules are available on [Ansible Galaxy website](https://galaxy.ansible.com/Juniper/junos/)   
- An Ansible library for Junos built by Ansible 
    - Since Ansible version >= 2.1, Ansible natively includes [core modules for Junos](http://docs.ansible.com/ansible/latest/list_of_network_modules.html#junos). 
  - These modules are shipped with Ansible
  - The Junos modules included in Ansible core have names which begin with the prefix **junos_**. 
  
These two sets of modules for Junos automation can coexist on the same Ansible control machine.  
Both of them are used in this repository.  

### Ansible modules for Junos built by Juniper and hosted on Galaxy

- They are hosted on the [Ansible Galaxy website](https://galaxy.ansible.com/Juniper/junos/)    
  - The role is Juniper.junos  
- Here's the [source code](https://github.com/Juniper/ansible-junos-stdlib)  
- Until the version 1.4.3 of the modules included in the Juniper.junos role
  - Their names begun with the prefix **junos_**. 
  - Here's the [doc for the version 1.4.3](http://junos-ansible-modules.readthedocs.io/en/1.4.3/)
  - To download and install them to the Ansible server, execute the command ```sudo ansible-galaxy install Juniper.junos,1.4.3```
- From version 2 of the modules included in the Juniper.junos role: 
  - To avoid conflict with the names used by ansible native modules for Junos, since the version 2 of the modules included in the Juniper.junos role on Galaxy, their names begin with the prefix **juniper_junos_**. 
  - Here's the [doc for the last version](http://junos-ansible-modules.readthedocs.io/en/stable/) 
  - To download and install them to the Ansible server, execute the command ```sudo ansible-galaxy install Juniper.junos```

### Ansible modules for Junos built and shipped by Ansible  

- Here's the [documentation](http://docs.ansible.com/ansible/latest/list_of_network_modules.html#junos)   
- The Junos modules included in Ansible core have names which begin with the prefix **junos_**. 
- Here's the [source code](https://github.com/ansible/ansible/tree/devel/lib/ansible/modules/network/junos)    
- Installation: They are shipped with ansible itself (from Ansible 2.1). Ansible 2.1 or above is required.  

### Requirements for Junos automation with Ansible  

##### On the Ansible server

Most of these Ansbile modules require to install the python library py-junos-eznc on the Ansible server.  
Some options require also to install the python library jxmlease on the Ansible server.  
Some options (like the console option in the junos_install_config module) require also the python library junos-netconify on the Ansible server.  

##### On the Junos devices

Except for the module junos_netconf, all the Ansible modules for Junos require the NETCONF to be configured on the Junos devices:
```
set system services netconf ssh
commit
```
Note: It is not required to use cli to configure Netconf on Junos devices. This can be done with the Ansible module junos_netconf. 

# How to use this repository  
 
### Get the content of the remote repository locally

```
sudo -s
git clone https://github.com/ksator/junos-automation-with-ansible.git
ls junos-automation-with-ansible
```

### Move to the local copy of the remote repo

```
cd junos-automation-with-ansible
sudo -s
```

### Install PyEZ, Jxmlease, Ansible, JSNAPy and all their dependencies

This repository has been tested using Ansible 2.4.2.0  

Run these commands on Ubuntu 16.04 to install these tools:
```
sudo -s
apt-get update
apt-get upgrade
apt-get install -y python-dev libxml2-dev python-pip libxslt1-dev build-essential libssl-dev libffi-dev git
pip install junos-eznc jxmlease wget jsnapy ansible==2.4.2.0 requests ipaddress cryptography 
ansible-galaxy install Juniper.junos,1.4.3
```
Check the Ansible version:
```
ansible --version
```
Verify you have the Juniper.junos role: 
```
ls /etc/ansible/roles/
```
This repository has been tested using the version 1.4.3 of the Juniper.junos role available on Galaxy.  
Use this command to see the name and version of each role installed:
```
ansible-galaxy list
```

You can now use the local copy of this remote repository.  
You need to run the below commands within the root of the project tree.

### Repository structure 
 
##### Inventory file:  

The default ```hosts``` file lives in ```/etc/ansible/hosts```.  

The inventory file we are using in this repository is [**hosts**](hosts). It is at the root of the repository, so it is not at the default place. 
It also defines the ip address of each device with the variable **junos_host**. This variable is re-used in the playbooks.     

##### Config file for ansible   
There is an [**ansible.cfg**](ansible.cfg) file at the root of the repository.  
It refers to our inventory file (**hosts**): So even if the inventory file is not /etc/ansible/hosts, there is no need to add ```-i hosts``` to your ```ansible-playbook``` commands.  

##### Variables  
[**group_vars**](group_vars) and [**host_vars**](host_vars) directories at the root of this repository define variables for hosts and for groups.  
The inventory file [**hosts**](hosts) at the root of the repository also defines some variables.   
The playbooks in this directory use all of them.   
Some playbooks use also other variables.  
In order to see all variables for a ```hostname```, you can run this command:  
```
ansible -m debug -a "var=hostvars['hostname']" localhost
```

##### Playbooks:  
All playbooks are named **pb*.yml**  
These playbooks use the modules from the two Ansible librairies to interact with Junos (the one built by Juniper and hosted on galaxy, and the core modules built by Ansible).  
They also use other Ansible modules (template, assemble, uri, wait_for, debug, ...).  
They are all ready-to-use if you access to the lab.    
You will find them in different directories.  

##### Directories:
Playbooks are in different directories.   
Each directory has a readme file as well. Please read the instructions in the readme.md file of each directory before executing the playbooks.    

##### Lab:  
The Junos devices we are using in this repository are in a lab which is only accessible from the Juniper Networks corporate network.   
The lab topology is described in the file [lab topology.pdf] (https://github.com/ksator/ansible-training-for-junos/blob/master/lab%20topology.pdf)  

You can very easily re-use this automation content with your own Junos devices (Junos physical devices, Junos virtual devices, vagrant boxes running Junos): you would just need to build a similar topology and to adapt this content with your IP addresses, username and password.   
If you want to build a Junos topology using Vagrant boxes, you can refer to this repository: https://github.com/ksator/vagrant-junos  

##### Branches:

There are currently 2 branches in this repository: 
- **master** - This is the original one, and the active one.   
- **topology_independent** - This is a new one. The topology_independent branch allows to use a different network topology without changing the playbooks. The automation content in this branch is probably not always up to date/in sync with the master branch.  

Here's how the **topology_independent** branch works: 

There is a file [topology.yml] (https://github.com/ksator/ansible-training-for-junos/blob/topology_independent/group_vars/all/topology.yml) in group_vars/all. This yaml file defines the topology. Here's an example:  
```
---
topo:
    ex4300-4:
        port1: { name: ge-0/0/0,     peer: ex4300-9,     pport: port2 }
        port2: { name: ge-0/0/1,     peer: ex4300-10,     pport: port2 }
        
    ex4300-9:
        port1: { name: ge-0/0/0,     peer: ex4300-10,     pport: port1 }
        port2: { name: ge-0/0/1,     peer: ex4300-4,     pport: port1 }
        
    ex4300-10:
        port1: { name: ge-0/0/0,    peer: ex4300-9,       pport: port1 }
        port2: { name: ge-0/0/1,    peer: ex4300-4,       pport: port2 }
```
This file is a dictionary with the key topo. The value of this key is the topology.  
Because this file is located in the directory group_vars/all, {{topo}} can be automatically used for all devices. 

Files in the host_vars directory were re-written.    
- **files in the host_vars directory in the master branch:**    
They are static. So if you use another network topology, it doesn’t work anymore until you rewrite these files.   
Example with https://github.com/ksator/ansible-training-for-junos/blob/master/host_vars/ex4300-10/bgp.yml  

```
---  
loopback: 10.20.1.3  
local_asn: 110
neighbors:
   - interface: ge-0/0/0
     name: ex4300-9
     asn: 109
     peer_ip: 192.168.0.5  
     local_ip: 192.168.0.4
     peer_loopback: 192.179.0.95
   - interface: ge-0/0/1 
     name: ex4300-4
     asn: 104
     peer_ip: 192.168.0.2
     local_ip: 192.168.0.3
     peer_loopback: 192.179.0.65
```
- **files in the host_vars directory in the topology_independent branch:**    
In the topology_independent branch, they use {{topo}}. So if we change the file [topology.yml] (https://github.com/ksator/ansible-training-for-junos/blob/topology_independent/group_vars/all/topology.yml), the content of the files in the host_vars directory change: no need to re-write it.   
Example with https://github.com/ksator/ansible-training-for-junos/blob/topology_independent/host_vars/ex4300-10/bgp.yml  

```
---
loopback: 10.20.1.3
local_asn: 110
neighbors:
   - interface: "{{ topo[inventory_hostname].port1.name }}"
     name: "{{ topo[inventory_hostname].port1.peer }}"
     asn: 109
     peer_ip: 192.168.0.5  
     local_ip: 192.168.0.4
     peer_loopback: 192.179.0.95
   - interface: "{{ topo[inventory_hostname].port2.name }}"
     name: "{{ topo[inventory_hostname].port2.peer }}"
     asn: 104
     peer_ip: 192.168.0.2
     local_ip: 192.168.0.3
     peer_loopback: 192.179.0.65
```

##### Installation instructions:  

Download the content:  
```
git clone https://github.com/ksator/ansible-training-for-junos.git  
```

And use ansible-playbook commands to execute the playbooks:    
```
cd ansible-training-for-junos/
ls
ls xxx/
more xxx/readme.md
ansible-playbook xxx/pb.*.yml  
```

##### Contributions, bugs, questions, enhancement requests:      
Please submit github issues or pull requests.  

### Continuous integration with Travis CI
There is a github webhook with Travis CI. 
The playbooks in  this repository are tested automatically by Travis CI.  
The files **.travis.yml** and **requirements.txt** at the root of this repository are used for this.  

We are using two types of playbooks in this repository:  

##### Some playbooks do not interact with Junos:   
Travis CI is testing them.  

##### Some playbooks interact with Junos:    
ansible-playbook has a built-in option to check only the playbook's syntax (--syntax-check). This is how Travis is testing the playbooks in this repositories that interact with Junos. If there is any syntax error, Travis will fail the build and output the errors in the log.  

### More examples on of how to use Ansible with Junos:   
For more examples, you can visit these repositories:   
https://github.com/JNPRAutomate/juniper_junos_ansible_modules_examples  
https://github.com/JNPRAutomate/ansible-junos-examples  
https://github.com/dgjnpr/ansible-template-for-junos  
https://github.com/JNPRAutomate/ansible-junos-evpn-vxlan    
https://github.com/JNPRAutomate/ansible-demo-ip-fabric   


### Looking for more Junos automation solutions:  

https://github.com/ksator?tab=repositories  
https://gitlab.com/users/ksator/projects  
https://gist.github.com/ksator/  

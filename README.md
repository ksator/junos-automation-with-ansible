[![Build Status](https://travis-ci.org/ksator/ansible-training-for-junos.svg?branch=master)](https://travis-ci.org/ksator/ansible-training-for-junos)  

#Ansible librairies to interact with Junos:  
There are two Ansible librairies to interact with Junos.  
- An Ansible library for Junos built by Juniper.  
- An Ansible library for Junos built by Ansible.  

Both of them are used into this repository.  

###Ansible modules for Junos built by Juniper:  
Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).    
Modules (version 1.4.0):     
- **junos_cli** - Execute CLI on device and save the output locally  
- **junos_commit** - Execute commit on device  
- **junos_get_config** - Retrieve configuration of device  
- **junos_get_facts** - Retrieve facts for a device running Junos OS. 
- **junos_get_table** - Retrieve data from a Junos device using Tables/Views
- **junos_install_config** - Load a configuration file or snippet onto a device running Junos OS.  
- **junos_install_os** - Install a Junos OS image. 
- **junos_jsnapy** - Execute JSNAPy test from Ansible
- **junos_rollback** - Rollback configuration of device  
- **junos_rpc** - run given rpc  
- **junos_shutdown** - Shut down or reboot a device running Junos OS.  
- **junos_srx_cluster** - Create an srx chassis cluster for cluster capable srx running Junos OS.
- **junos_ping** - execute ping on junos devices
- **junos_zeroize** - Erase all data, including configuration and log files, on a device running Junos OS.  

Documentation: http://junos-ansible-modules.readthedocs.io/  
Source code: https://github.com/Juniper/ansible-junos-stdlib  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).  
To download them to the Ansible server, execute the command:   
```
sudo ansible-galaxy install Juniper.junos  
```

###Ansible core modules for Junos built by Ansible:   

Modules (Ansible 2.1.1.0):   
- **junos_command** - Execute arbitrary commands on a remote device running Junos  
- **junos_config** - Manage configuration on remote devices running Junos  
- **junos_facts** - Collect facts from remote device running Junos  
- **junos_netconf** - Configures the Junos Netconf system service  
- **junos_package** - Installs packages on remote devices running Junos  
- **junos_template** - Manage configuration on remote devices running Junos  

Documentation: http://docs.ansible.com/ansible/list_of_network_modules.html    
Installation: core modules. They ship with ansible itself (from Ansible 2.1). Ansible 2.1 or above is required.    
Source code: https://github.com/ansible/ansible-modules-core/tree/devel/network/junos  

###Requirements:  

##### On the Ansible server:

Most of these Ansbile modules require to install the python library py-junos-eznc on the Ansible server.  
Some options (like the console option in the junos_install_config module) require also the python library junos-netconify.

##### On the Junos devices:

Except for the module junos_netconf, all these Ansible modules for Junos require the Netconf API to be configured on the Junos devices:
```
set system services netconf ssh
commit
```
Note: It is not required to use cli to configure Netconf on Junos devices. This can be done with the Ansible module junos_netconf. 

#About this project:   
This project has many ready to use Ansible playbooks to interact with Junos devices.    
I am using them to deliver Ansible trainings to network engineers.  

There is an Ansible presentation available in this repository: [Ansible presentation.pdf] (https://github.com/ksator/ansible-training-for-junos/blob/master/Ansible%20presentation.pdf)  
 
###How to use this project: 

The playbooks in this repository are ready to use if you access to the Junos devices refered into this project. 

#####Inventory file:  
The default 'hosts' file is supposed to live in /etc/ansible/hosts  
The inventory file we are using in this repository is **hosts**. It is at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/hosts), so it is not at the default place.  
it also define the ip address of each device with the variable **junos_host**. This variable is reused in the playbooks.     

#####Config file for ansible:   
There is an **ansible.cfg** file at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/ansible.cfg).  
It refers to our inventory file (**hosts**): So, despite the inventory file is not /etc/ansible/hosts, there is no need to add -i hosts to your ansible-playbook commands.  

#####Variables:   
**group_vars** and **host_vars** directories at the root of this repository define variables for hosts and for groups.  
The inventory file (**hosts** file at the root of the repository) also defines some variables.   
Our playbooks use all of them.   
Some playbooks use also other variables.  

#####Playbooks:  
All playbooks are named **pb.*.yml**  
These playbooks use the modules from the two Ansible librairies to interact with Junos (the one built by Juniper and hosted on galaxy, and the core modules built by Ansible).  
They also use other Ansible modules (template, assemble, uri, wait_for, debug, ...).  
They are all ready to use if you access to the lab.    
You will find them into different directories.  

#####Directories:
Playbooks are in different directories.   
Each directory has a readme file as well. Please read the instructions in the readme.md file of each directory before executing the playbooks.    

#####Lab:  
The Junos devices we are using in this repository are in a lab which is only accessible from the Juniper Networks corporate network.   
The lab topology is described in the file [lab topology.pdf] (https://github.com/ksator/ansible-training-for-junos/blob/master/lab%20topology.pdf)  

You can very easily reuse this automation content with your own Junos devices (Junos physical devices, Junos virtual devices, vagrant boxes running Junos): you would just need to build a similar topology and to adapt this content with your IP addresses, username and password.   
If you want to build a Junos topology using Vagrant boxes, you can refer to this repository: https://github.com/ksator/vagrant-junos  

#####Branches:

There are currently 2 branches into this repository: 
- **master** - This is the original one, and the active one.   
- **topology_independent** - This is a new one. The topology_independent branch allows to use a different network topology without changing the playbooks. The automation content into this branch is probably not always up to date/in sync with the master branch.  

Here's how the **topology_independent** branch works: 

There is a file [topology.yml] (https://github.com/ksator/ansible-training-for-junos/blob/topology_independent/group_vars/all/topology.yml) into group_vars/all. This yaml file defines the topology. here's an example:  
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
This file is a dictionnary with the key topo. The value of this key is the topology.  
Because this file is located into the directory group_vars/all, {{topo}} can be automatically used for all devices. 

Files in the host_vars directory were rewrited.    
- **files in the host_vars directory in the master branch:**    
They are static. So if you use another network topology, it doesnt work anymore until you rewrite these files.   
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
in the topology_independent branch, they use {{topo}}. So if we change the file [topology.yml] (https://github.com/ksator/ansible-training-for-junos/blob/topology_independent/group_vars/all/topology.yml), the content of the files in the host_vars directory change: no need to rewrite it.   
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

#####Installation instructions:  

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

#####Some playbooks do not interact with Junos:   
Travis CI is testing them.  

#####Some playbooks interact with Junos:    
ansible-playbook has a built in option to check only the playbook's syntax (--syntax-check). This is how Travis is testing our playbooks that interact with Junos. If there are any syntax error, Travis will fail the build and output the errors in the log.  

### More examples on of how to use Ansible with Junos:   
For more examples, you can visit these repositories:   
https://github.com/JNPRAutomate/ansible-junos-examples  
https://github.com/dgjnpr/ansible-template-for-junos  
https://github.com/JNPRAutomate/ansible-junos-evpn-vxlan    
https://github.com/JNPRAutomate/ansible-demo-ip-fabric  



[![Build Status](https://travis-ci.org/ksator/ansible-training-for-junos.svg?branch=master)](https://travis-ci.org/ksator/ansible-training-for-junos)  

#Ansible librairies to interact with Junos:  
There are two Ansible librairies to interact with Junos.  
- An Ansible library for Junos built by Juniper.  
- An Ansible library for Junos built by Ansible.  

Both of the Ansible libraries for Junos are used into this repository.  

###Ansible modules for Junos built by Juniper:  

Modules (version 1.3.1):     
- **junos_cli** - Execute CLI on device and save the output locally  
- **junos_commit** - Execute commit on device  
- **junos_get_config** - Retrieve configuration of device  
- **junos_get_facts** - Retrieve facts for a device running Junos OS.  
- **junos_install_config** - Load a configuration file or snippet onto a device running Junos OS.  
- **junos_install_os** - Install a Junos OS image.  
- **junos_rollback** - Rollback configuration of device  
- **junos_rpc** - run given rpc  
- **junos_shutdown** - Shut down or reboot a device running Junos OS.  
- **junos_srx_cluster** - Create an srx chassis cluster for cluster capable srx running Junos OS.  
- **junos_zeroize** - Erase all data, including configuration and log files, on a device running Junos OS.  

Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Source code: https://github.com/Juniper/ansible-junos-stdlib  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download them to the Ansible server, execute the command:   
```
sudo ansible-galaxy install Juniper.junos  
```

###Ansible core modules for Junos built by Ansible:   

Modules (Ansible 2.1):   
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

Most of these Ansible modules for Junos require the Netconf API to be configured on the Junos devices:
```
set system services netconf ssh
commit
```

#About this project:   
This project has many ready to use Ansible playbooks to interact with Junos devices.    
I am using them to deliver Ansible trainings to network engineers.  

###How to use this project: 

#####Lab:  
The playbooks in this repository are ready to use if you access to the Junos devices refered into this project. 
The Junos devices we are using in this repository are only accessible from the Juniper Networks corporate network.   

But you can very easily reuse this automation content with your own Junos devices (Junos physical devices, Junos virtual devices, vagrant boxes running Junos): you would just need to adapt this content with your IP addresses, username and password.   
If you want to build a Junos topology using Vagrant boxes, you can use this repository: https://github.com/ksator/vagrant-junos    

#####Inventory file:  
The default ansible 'hosts' file is supposed to live in /etc/ansible/hosts  
The inventory file we are using in this repository is **hosts**: It is at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/hosts), so it is not at the default place.   

#####Config file for ansible:   
There is an **ansible.cfg** file at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/ansible.cfg).  
It refers to our inventory file (**hosts**): So, despite the inventory file is not /etc/ansible/hosts, there is no need to add -i hosts to your ansible-playbook commands.  

#####Variables:   
**group_vars** and **host_vars** directories at the root of this repository define variables for hosts and for groups. 
Some playbooks use other variables as well. 

#####Playbooks:  
All playbooks are named **pb.*.yml**  
You will find them in different directories. Each directory has a readme file as well.    

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

### Continuous integration with Travis CI
There is a github webhook with Travis CI. 
The playbooks in  this repository are tested by Travis CI, with several Ansible versions. 
The files **.travis.yml** and **requirements.txt** at the root of this repository are used for this.  

We are using two types of playbooks in this repository:  

#####Some playbooks do not interact with Junos:   
Travis CI is testing them.  

#####Some playbooks interact with Junos:    
ansible-playbook has a built in option (--syntax-check) to check the playbook's syntax. If there are any syntax error, Travis will fail the build and output the errors in the log. This is how Travis is testing our playbooks that interact with Junos.  

### More examples on of how to use Ansible with Junos:   
For more examples on of how to use Ansible with Junos, you can visit these repositories:   
https://github.com/JNPRAutomate/ansible-junos-examples  
https://github.com/dgjnpr/ansible-template-for-junos  
https://github.com/JNPRAutomate/ansible-junos-evpn-vxlan    
https://github.com/JNPRAutomate/ansible-demo-ip-fabric  





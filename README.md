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
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download them to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Source code: https://github.com/Juniper/ansible-junos-stdlib  

###Ansible modules for Junos built by Ansible:   

Modules (Ansible 2.1):   
- **junos_command** - Execute arbitrary commands on a remote device running Junos  
- **junos_config** - Manage configuration on remote devices running Junos  
- **junos_facts** - Collect facts from remote device running Junos  
- **junos_netconf** - Configures the Junos Netconf system service  
- **junos_package** - Installs packages on remote devices running Junos  
- **junos_template** - Manage configuration on remote devices running Junos  

Documentation: http://docs.ansible.com/ansible/list_of_network_modules.html    
Installation: core modules. They ship with ansible itself (from Ansible 2.1)  
Source code: https://github.com/ansible/ansible-modules-core/tree/devel/network/junos  

###Requirements:  
Most of these modules requires to install on the Ansible server the pytthon librairy py-junos-eznc.  
Some requires also junos-netconify.  

#About this project:   
This project has many ready to use Ansible playbooks to interact with Junos devices.    
All playbooks are named pb.*.yaml  

###How to use this project: 

#####Inventory file:  
The default ansible 'hosts' file is supposed to live in /etc/ansible/hosts  
The inventory file we are using in this repository is hosts: It is at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/hosts), so it is not at the default place.   

#####Config file for ansible:   
There is an ansible.cfg file at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/ansible.cfg).  
It refers to our inventory file (hosts): So, despite the inventory file is not /etc/ansible/hosts, there is no need to add -i hosts to your ansible-playbook commands.  

#####Installation instructions:  

Download the content:  
```
git clone https://github.com/ksator/ansible-training-for-junos.git  
```

And use ansible-playbook commands to execute playbooks:    
All playbooks are named pb.*.yaml  
```
cd ansible-training-for-junos/    
ansible-playbook xxx/pb.yml  
```

### continuous-integration with Travis CI
There is a github webhook with Travis CI. 
The playbooks in  this repository are tested by Travis CI, with several Ansible versions. 

We are using two types of playbooks:

#####Some playbooks do not interact with Junos:   
Travis CI is testing them.  

#####Some playbooks interact with Junos.  
ansible-playbook has a built in option (--syntax-check) to check the playbook's syntax. If there are any syntax error, Travis will fail the build and output the errors in the log. This is how Travis is testing our playbooks that interact with Junos.  

### More examples on of how to use Ansible with Junos:   
For more examples on of how to use Ansible with Junos, you can visit these repositories:   
https://github.com/JNPRAutomate/ansible-junos-examples  
https://github.com/JNPRAutomate/ansible-junos-evpn-vxlan    
https://github.com/JNPRAutomate/ansible-demo-ip-fabric  
https://github.com/dgjnpr/ansible-template-for-junos  



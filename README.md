#About this project:   
This project has many ready to use Ansible playbooks to interact with Junos devices.    

##Ansible librairies to interact with Junos:  
There are two Ansible librairies to interact with Junos.
An Ansible library for Junos built by Juniper.  
An Ansible library for Junos built by Ansible.  
Both of the Ansible libraries for Junos are used into this repository.  

###Ansible modules for Junos built by Juniper:  
doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
installation: this is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
source code: https://github.com/Juniper/ansible-junos-stdlib  

###Ansible modules for Junos built by Ansible:   
doc: http://docs.ansible.com/ansible/list_of_network_modules.html    
installation: core modules. They ship with ansible itself (from Ansible 2.1)  
source code: https://github.com/ansible/ansible-modules-core/tree/devel/network/junos  

###Requirements: 
Most of these modules requires to install on the Ansible server the pytthon librairy py-junos-eznc.  
Some requires also junos-netconify.  

##How to use this project: 

###Inventory file:  
The default ansible 'hosts' file is supposed to live in /etc/ansible/hosts  
The inventory file we are using in this repository is hosts.   
It is at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/hosts), so it is not at the default place.   

###Config file for ansible:   
There is an ansible.cfg file at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/ansible.cfg) that refers to this inventory file.   
So, despite ithe inventory file is not /etc/ansible/hosts, there is no need to add -i hosts to your ansible-playbook commands.  

###Download the content:  
git clone https://github.com/ksator/ansible-training-for-junos.git  
cd ansible-training-for-junos/    

###And use ansible-playbook commands to execute playbooks:    
ansible-playbook xxx/pb.yml  






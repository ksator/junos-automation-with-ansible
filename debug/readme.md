Module: debug  
Doc: http://docs.ansible.com/ansible/debug_module.html  
you can use this module to print something during playbook execution. Useful for debugging  
Installation: this is a core module. It ships with ansible itself  

module: junos_get_facts  
doc: http://junos-ansible-modules.readthedocs.io/  
Retrieve facts for a device running Junos OS, which includes information such as the serial number, product model, Junos OS version ...   
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).   
To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
requirements on Junos devices: netconf  
requirements on Ansible: junos-eznc.  junos-netconify when using the console optional argument.    

Playbooks:  
- **pb.yml**: this playbook get the junos facts from a group of junos devices, and print the hostname of the devices that are not running a specific junos version.     

Usage: 
```
sudo ansible-playbook debug/pb.yml   
```

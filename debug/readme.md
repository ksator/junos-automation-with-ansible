Module: debug  
Installation: this is a core module. It ships with ansible itself  
Doc: http://docs.ansible.com/ansible/debug_module.html  

Playbooks:
- pb.yml: this playbook get the junos facts from a group of junos devices, and print the hostname of the devices that are not running a specific junos version.     

Usage: 
```
sudo ansible-playbook debug/pb.yml   
```

module: debug  
installation: it is a core module  
doc: http://docs.ansible.com/ansible/debug_module.html  

pb.yml: this playbook get the junos facts from a group of junos devices, and print the hostname of the devices that are not running a specific junos version.     
usage: 
```
sudo ansible-playbook debug/pb.yml   
```

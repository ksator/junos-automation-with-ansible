module: junos_get_facts  
doc: http://junos-ansible-modules.readthedocs.io/  
Retrieve facts for a device running Junos OS, which includes information such as the serial number, product model, Junos OS version ... 
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Requirements on Ansible: junos-eznc
Requirements on Junos devices: netconf 

playbooks: 
- **pb.yml**: get some facts from junos devices.  Save them locally. Print devices hostname if they are not running 12.3R11.2

usage: 
```
ansible-playbook junos_get_facts/pb.yml
ls -l junos_get_facts/inventory/
more junos_get_facts/inventory/ex4200-10-facts.json
```

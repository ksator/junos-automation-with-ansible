Module: junos_netconf  
This module uses SSH to configure netconf on Junos devices.   
Documentation: http://docs.ansible.com/ansible/junos_netconf_module.html  
Installation: this is a core module. It ships with ansible itself   

Playbooks:
- **pb.yml**: it uses SSH to configure NETCONF on port 830  

Usage:
```
ansible-playbook junos_netconf/pb.yml --check  --diff
```
```
ansible-playbook junos_netconf/pb.yml  
```

Module: junos_netconf  
This module configures netconf on Junos devices.   
Documentation: http://docs.ansible.com/ansible/junos_netconf_module.html  
Installation: this is a core module. It ships with ansible itself   
Requirement: Ansible 2.1. it doesnt use junos-eznc on Ansible. it doesnt use netconf on Junos devices. 

Playbooks:
- **pb.yml**: it configures the Netconf API on Junos devices on port 830 (default Netconf port, RFC 6242).  

Usage:
```
ansible-playbook junos_netconf/pb.yml --check   
ansible-playbook junos_netconf/pb.yml --check --diff
ansible-playbook junos_netconf/pb.yml  
```

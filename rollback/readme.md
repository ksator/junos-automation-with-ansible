Module: junos_rollback  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download itto the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: enable netconf on junos.  

Playbooks: 
- pb.yml: it rollbacks Junos configuration on junos devices.  

Usage: 
```
ansible-playbook rollback/pb.yml  
```

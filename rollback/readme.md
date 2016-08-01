Module: junos_rollback  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Documentation: http://junos-ansible-modules.readthedocs.io/ 
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  


Playbooks: 
- pb.yml: it rollbacks Junos configuration on junos devices (rollback 1 the group AMS-EX4300).  

Usage: 
```
ansible-playbook rollback/pb.yml
ls -l rollback/
more rollback/172.30.179.65.diff
```

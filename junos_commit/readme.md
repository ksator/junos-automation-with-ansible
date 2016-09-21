Module: junos_commit  
Documentation: http://junos-ansible-modules.readthedocs.io/  
The use case is to confirm a previous commit confirm (before the automatic rollback).   
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Requirement on Junos devices: enable netconf.  
Requirements on Ansible: junos-eznc

playbooks: 
- **pb.yml**: Execute a commit on a group of Junos devices independently of loading a configuration. 

Usage: 
```
ansible-playbook junos_commit/pb.yml  
```

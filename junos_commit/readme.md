Module: junos_commit  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: enable netconf on junos.  

playbooks: 
- pb.yml: Execute a commit on Junos devices independently of loading a configuration. The use case is to confirm a previous commit confirm.   

Usage: 
```
ansible-playbook junos_commit/pb.yml  
```

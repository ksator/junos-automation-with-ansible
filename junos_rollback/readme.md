Module: junos_rollback  
Rollback the configuration of a device running Junos  
Documentation: http://junos-ansible-modules.readthedocs.io/  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).   
To download it to the Ansible server, execute the command: 
```
ansible-galaxy install Juniper.junos  
```
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  


Playbooks: 
- pb.yml: it rollbacks Junos configuration on junos devices (rollback 1 the group AMS-EX4300).  

Usage: 
```
ansible-playbook junos_template/pb.change_dns_servers.yml --diff --skip-tags "Retrieve configuration"
ansible-playbook rollback/pb.yml
ls -l rollback/
more rollback/ex4300-9.diff
```

Module: junos_install_config  
Doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  

playbooks:
- Pb.yml: install configuration files on junos devices.  

Usage:  
```
ansible-playbook junos_install_conf/pb.yml  
```

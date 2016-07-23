Module: junos_install_config  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: Enable netconf on junos.   

playbooks:
- Pb.yml: install configuration files on junos devices.  

Usage:  
```
ansible-playbook install_conf/pb.yml  
```

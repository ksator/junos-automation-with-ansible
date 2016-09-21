Module: junos_install_config  
Doc: http://junos-ansible-modules.readthedocs.io/  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  

playbooks:
- **Pb.yml**: install a list of configuration files on junos devices (2 files: syslog.set and banner.set, this makes 2 separate commit, one per file).   

Usage:  
```
ansible-playbook junos_install_conf/pb.yml  --check
ansible-playbook junos_install_conf/pb.yml  --check --diff
ansible-playbook junos_install_conf/pb.yml  
ls -l junos_install_conf/
more junos_install_conf/install_config.log
ansible-playbook junos_install_conf/pb.yml  --check --diff
```

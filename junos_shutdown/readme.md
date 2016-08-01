Module: junos_shutdown  
Shut down or reboot a device running Junos OS.  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command:   
```
sudo ansible-galaxy install Juniper.junos  
```
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos. 


Playbooks:  
- **pb.yml**: this playbook reboots a Junos device

Usage:  
```
ansible-playbook junos_shutdown/pb.yml
```

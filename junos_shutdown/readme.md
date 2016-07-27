Module: junos_shutdown
Shut down or reboot a device running Junos OS.
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: 
```
sudo ansible-galaxy install Juniper.junos  
```
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: enable netconf on junos.  

Playbooks:
- pb.yml: reboot a Junos device

Usage:   
```
ansible-playbook junos_shutdown/pb.yml

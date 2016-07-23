Module: junos_get_config  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: enable netconf on junos.  

Playbooks: 
- pb.junos_get_config.yml: it retrieves junos configuration from junos devices and save it to a file in the configs directory on the Ansible server. This will fail if the configs directory doesnt exist.  
- pb.make_clean.yml: it makes sure the configs directory exist, and removes the old files from the configs directory for each host.  
- pb.yml: it includes pb.make_clean.yml and pb.junos_get_config.yml.  
- pb.2.yml: it does the same thing as pb.yml, with a different filter (so it retrieves another part of the junos configuration file)  
 
Usage:
```
ansible-playbook junos_get_config/pb.yml  
ansible-playbook junos_get_config/pb.2.yml  
```

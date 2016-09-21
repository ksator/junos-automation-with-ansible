Module: junos_get_config  
Documentation: http://junos-ansible-modules.readthedocs.io/  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf  

Playbooks: 
- **pb.junos_get_config.yml**: It retrieves junos configuration from junos devices and save it to a file in the configs directory on the Ansible server. This will fail if the configs directory doesnt exist on the Ansible server.
- **pb.make_clean.yml**: It makes sure the configs directory exist, and removes the old files from the configs directory for each host.  
- **pb.yml**: it includes pb.make_clean.yml and pb.junos_get_config.yml playbooks.  
- **pb.2.yml**: it does the same thing as pb.yml, with a different filter (so it retrieves another part of the junos configuration file)  
 
Usage:
```
ansible-playbook junos_get_config/pb.2.yml  
ls -l junos_get_config/configs/
more junos_get_config/configs/ex4200-9.conf
more junos_get_config/junos_get_config.log

ansible-playbook junos_get_config/pb.yml  
ls -l junos_get_config/configs/
more junos_get_config/configs/ex4200-9.conf
more junos_get_config/junos_get_config.log
```

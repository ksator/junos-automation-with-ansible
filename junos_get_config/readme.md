module: junos_get_config  
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  

playbooks: Retrieve the configuration of a Junos devices and save it to a file  
requirement: enable netconf on junos.  
usages:    
ansible-playbook junos_get_config/pb.yml  
ansible-playbook junos_get_config/pb.2.yml  

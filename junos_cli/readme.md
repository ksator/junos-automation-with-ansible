module: junos_cli  
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  

playbooks: pass cli to junos devices.  
requirement: enable netconf on junos.  
usages:   
ansible-playbook junos_cli/pb.txt.yml -i hosts  
ansible-playbook junos_cli/pb.xml.yml -i hosts  



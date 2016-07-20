module: junos_commit  
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  

playbooks: Execute a commit on Junos devices independently of loading a configuration. use case is to confirm a commit confirm.   
requirement: enable netconf on junos.  
usage: ansible-playbook junos_commit/pb.yml  

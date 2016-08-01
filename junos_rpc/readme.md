Module: junos_rpc  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Doc: http://junos-ansible-modules.readthedocs.io/
Requirement on Ansible: junos-eznc
Requirement on Junos devices: enable netconf on junos. 

Playbooks: 
- **pb.yml**: it passes an rpc to junos devices and save the output on the Ansible server.  


Usage: 
```
ansible-playbook junos_rpc/pb.yml  
ls -l junos_rpc/
more junos_rpc/172.30.179.102.conf
```

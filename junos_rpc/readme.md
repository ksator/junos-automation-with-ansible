Module: junos_rpc  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: Enable netconf on junos.  

Playbooks: 
- pb.yml: it passes an rpc to junos devices and save the output on the Ansible server.  


Usage: 
```
ansible-playbook junos_rpc/pb.yml  
```

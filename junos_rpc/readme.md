Module: junos_rpc  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Doc: http://junos-ansible-modules.readthedocs.io/  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos. 

Playbooks: 
- **pb.yml**: it passes an rpc to junos devices and save the output on the Ansible server. 
- **pb.2.yml**: it passes an rpc with arguments to a junos device, and print the rpc reply in json 

Usage: 
```
ansible-playbook junos_rpc/pb.yml  
ls -l junos_rpc/
more junos_rpc/ex4200-11.conf

ansible-playbook junos_rpc/pb.2.yml  
```

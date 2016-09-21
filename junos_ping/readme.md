Module: junos_ping
Description: Execute ping on junos devices
Documentation: http://junos-ansible-modules.readthedocs.io/
Source code: https://github.com/Juniper/ansible-junos-stdlib/tree/master/library  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos
Requirement on Ansible: junos-eznc
Requirements on Junos devices: netconf

Playbooks:  
- **pb.yml**: check if your junos devices can ping some remote ip addresses. You first need to configure some routing details on your devices. You can use one of these BGP playbooks to configure BGP on your devices https://github.com/ksator/ansible-training-for-junos/tree/master/junos_template


Usage:
```
ansible-playbook junos_template/pb.bgp.2.yml
ansible-playbook junos_ping/pb.yml
ansible-playbook rollback/pb.yml
```


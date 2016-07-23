Module: junos_cli  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
Requirement: enable netconf on junos.  

Playbooks:
- pb.txt.yml: pass cli to junos devices. Save output in text format  
- pb.xml.yml: pass cli to junos devices. Save output in XML format  

Usage:   
```
ansible-playbook junos_cli/pb.txt.yml   
ansible-playbook junos_cli/pb.xml.yml    
```


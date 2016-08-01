Module: junos_cli  
Documentation: http://junos-ansible-modules.readthedocs.io/    
Execute CLI on device and save the output on Ansible    
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  



Playbooks:
- **pb.txt.yml**: pass cli to junos devices. Save output in text format  
- **pb.xml.yml**: pass cli to junos devices. Save output in XML format  

Usage:   
```
ansible-playbook junos_cli/pb.txt.yml
ls junos_cli/
more junos_cli/172.30.179.108.txt
more junos_cli/cli.log

ansible-playbook junos_cli/pb.xml.yml
ls junos_cli/
more junos_cli/172.30.179.108.xml
```


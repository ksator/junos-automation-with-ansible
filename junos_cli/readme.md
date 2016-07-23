module: junos_cli  
installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
requirement: enable netconf on junos.  

playbooks:
- pb.txt.yml: pass cli to junos devices. Save output saved in text format  
- pb.xml.yml: pass cli to junos devices. Save output saved in XML format  

usages:   
```
ansible-playbook junos_cli/pb.txt.yml   
ansible-playbook junos_cli/pb.xml.yml    
```


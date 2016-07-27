Module: template   
Installation: this is a core module. It ships with ansible itself  
Documentation : http://docs.ansible.com/ansible/template_module.html  

Playbooks:  
- pb.initial_configuration.yml: create junos configuration for new devices based on the template initial_configuration.j2. The junos configuration files created are stored in the directory render

Usage:   
```
ansible-playbook template/pb.initial_configuration.yml
ls template/render/
```

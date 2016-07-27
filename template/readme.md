Module: template   
it creates a document based on a Jinja2 template.  
Documentation : http://docs.ansible.com/ansible/template_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  
- pb.initial_configuration.yml: create junos configuration for new devices based on the template initial_configuration.j2. The junos configuration files created are stored in the directory render
- pb.common_settings.yml: create junos configuration for common settings (syslog, ntp, snmp...) based on the template common_settings.j2. The junos configuration files created are stored in the directory render

Usage:   
```
ansible-playbook template/pb.initial_configuration.yml
ls template/render/

ansible-playbook template/pb.common_settings.yml
ls template/render/
```

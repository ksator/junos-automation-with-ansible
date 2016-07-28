Module: junos_template  
Load a configuration file to Junos devices. The source can be either a configuration file or a jinja 2 template that is automatically rendered.  
Documentation: http://docs.ansible.com/ansible/junos_template_module.html  
Installation: this is a core module. It ships with ansible itself   
Requirements on Ansible: Ansible 2.1 and junos-eznc  
Requirements on  Junos devices: netconf  

Playbooks:  
- pb.bgp.yml: It load a configuration file to Junos devices. The source can be either a configuartion file or a jinja 2 template that is automatically rendered.  
- pb.bgp.2.yml: The same task renders a jinja2 template with BGP details and loads it to Junos devices. Another task in the same playbook audit the states of the BGP neighbors. it does the same thing as pb.bgp.yml but we splitted into two separate tasks the template rendering (so we can have a copy of the document) and the loading configuration.  

Usage:
```
ansible-playbook junos_template/pb.bgp.yml --limit 172.30.179.65 --tags "configuration" --check --diff  
ansible-playbook junos_template/pb.bgp.yml  

ansible-playbook junos_template/pb.bgp.2.yml  
ls junos_template/render/   
```

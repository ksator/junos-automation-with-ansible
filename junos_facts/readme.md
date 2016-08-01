Module: junos_facts  
Collect facts from Junos devices. The configuration can be collected as well.  
Documentation: http://docs.ansible.com/ansible/junos_facts_module.html  
source code: https://github.com/ansible/ansible-modules-core/tree/devel/network/junos   
Installation: this is a core module. It ships with ansible itself   
Requirements on Ansible: Ansible 2.1 and junos-eznc   
Requirements on  Junos devices: netconf  

Playbooks:  
- **pb.facts.yml**: Collect facts. Parse them.    
- **pb.conf.yml**: collect configuration.   
- **pb.conf_json_and_xml.yml**: Collect Facts and Configuration. Print locally configuration in XML and JSON format.  
- **pb.conf.txt.yaml**: Collect facts and configuration. Save locally the configuration in text format.   

Usage:  
```
ansible-playbook junos_facts/pb.conf.txt.yaml
ls junos_facts/
more junos_facts/ex4200-11.conf

ansible-playbook junos_facts/pb.facts.yml
ansible-playbook junos_facts/pb.conf.yml
ansible-playbook junos_facts/pb.conf_json_and_xml.yml
```

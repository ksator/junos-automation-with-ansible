Module: template   
it creates a document based on a Jinja2 template.  
Documentation : http://docs.ansible.com/ansible/template_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  
- **pb.initial_configuration.yml**: create junos configuration for new devices based on the template **initial_configuration.j2**. The junos configuration files created are stored in the directory render
- **pb.common_settings.yml**: create junos configuration for common settings (syslog, ntp, snmp...) based on the template **common_settings.j2**. The junos configuration files created are stored in the directory render
- **pb.bgp.yml**: create Junos BGP configuration based on the template **bgp.j2**. The junos configuration files created are stored in the directory render
- **pb.load_cfg_from_template.yml**: use the template **dns-servers.j2** and the variables **dns-servers.yml** to create a Junos configuration file to add DNS servers, and apply the document to Junos devices. This playbook adds DNS servers to the existing configuration on devices. 
- **pb.load_cfg_from_template.replace.yml**: use the template **dns-servers.replace.j2** and the variables **dns-servers.yml** to create a Junos configuration file to add DNS servers, and apply the document to Junos devices. This playbook replace the DNS configuration on devices. 

Usage:   
```
ansible-playbook template/pb.initial_configuration.yml
ls template/render/

ansible-playbook template/pb.common_settings.yml
ls template/render/

ansible-playbook template/pb.bgp.yml
ls template/render/

ansible-playbook template/pb.load_cfg_from_template.yml
ls template/render/
ls template/
ansible-playbook rollback/pb.yml

ansible-playbook template/pb.load_cfg_from_template.replace.yml
ls template/render/
ls template/
ansible-playbook rollback/pb.yml
```

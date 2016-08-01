Module: template   
it creates a document based on a Jinja2 template.  
Documentation : http://docs.ansible.com/ansible/template_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  
- **pb.initial_configuration.yml**: create junos configuration for new devices based on the template **initial_configuration.j2**. The junos configuration files created are stored in the directory render. Nothing is loaded on Junos devices.  
- **pb.common_settings.yml**: create junos configuration for common settings (syslog, ntp, snmp...) based on the template **common_settings.j2**. The junos configuration files created are stored in the directory render. Nothing is loaded on Junos devices.  
- **pb.bgp.yml**: create Junos BGP configuration based on the template **bgp.j2**. The junos configuration files created are stored in the directory render. Nothing is loaded on Junos devices.  
- **pb.load_cfg_from_template.yml**: use the template **dns-servers.j2** and the variables **dns-servers.yml** to create a Junos configuration file to add DNS servers, and apply the document to Junos devices. This playbook adds DNS servers to the existing configuration on devices. 
- **pb.load_cfg_from_template.replace.yml**: use the template **dns-servers.replace.j2** and the variables **dns-servers.yml** to create a Junos configuration file to add DNS servers, and apply the document to Junos devices. This playbook replace the DNS configuration on devices. 

Usage:   
```
ansible-playbook template/pb.common_settings.yml
ls -l template/render/*common_settings.conf
more template/render/ex4300-10.common_settings.conf

ansible-playbook template/pb.initial_configuration.yml --check
ansible-playbook template/pb.initial_configuration.yml --check --diff
ansible-playbook template/pb.initial_configuration.yml
ls -l template/render/*initial_configuration.conf
more template/render/ex4300-10.initial_configuration.conf

ansible-playbook template/pb.bgp.yml --check --diff --limit 172.30.179.65
ansible-playbook template/pb.bgp.yml
ls -l template/render/*.bgp.conf
more template/render/ex4300-10.bgp.conf

ansible-playbook template/pb.load_cfg_from_template.yml --check --diff
ansible-playbook template/pb.load_cfg_from_template.yml
ls -l template/render/*.conf
more template/render/ex4300-10.conf
ls -l template/*.log
more template/ex4300-10.log
ansible-playbook rollback/pb.yml

ansible-playbook template/pb.load_cfg_from_template.replace.yml --check --diff
ansible-playbook template/pb.load_cfg_from_template.replace.yml
ls -l template/render/*.conf
more template/render/ex4300-10.conf
ls -l template/*.log
more template/ex4300-10.log
ansible-playbook rollback/pb.yml
```

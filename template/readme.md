Module: template   
it creates a document based on a Jinja2 template.  
Documentation : http://docs.ansible.com/ansible/template_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  

- **pb_render_initial_configuration.yml**: creates junos configuration for new devices based on the template **initial_configuration.j2**. The junos configuration files created are stored in the directory **render**. Nothing is loaded on Junos devices.  
- **pb_render_common_settings.yml**: creates junos configuration for common settings (syslog, ntp, snmp...) based on the template **common_settings.j2**. The junos configuration files created are stored in the directory **render**. Nothing is loaded on Junos devices.  
- **pb_render_bgp.yml**: creates Junos BGP configuration based on the template **bgp.j2**. The junos configuration files created are stored in the directory **render**. Nothing is loaded on Junos devices.  
- **pb_load_cfg_from_template.yml**: uses the template **dns-servers.j2** and the variables **dns-servers.yml** to create a Junos configuration file to add DNS servers, and applies the document to Junos devices. This playbook adds DNS servers to the existing configuration on devices. 
- **pb_load_cfg_from_template_replace.yml**: uses the template **dns-servers_replace.j2** and the variables **dns-servers.yml** to create a Junos configuration file to add DNS servers, and applies the document to Junos devices. This playbook replaces the DNS configuration on devices. The diff is saved in the directory **diff**

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
ansible-playbook junos_rollback/pb.yml

ansible-playbook template/pb.load_cfg_from_template.replace.yml --check --diff
ansible-playbook template/pb.load_cfg_from_template.replace.yml
ls -l template/render/*.conf
more template/render/ex4300-10.conf
ls -l template/*.log
more template/ex4300-10.log
ansible-playbook junos_rollback/pb.yml
```
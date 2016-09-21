Module: junos_template  
Load a configuration file to Junos devices. The source can be either a configuration file or a jinja 2 template that is automatically rendered.  
Documentation: http://docs.ansible.com/ansible/junos_template_module.html  
Installation: this is a core module. It ships with ansible itself   
Requirements on Ansible: Ansible 2.1 and junos-eznc  
Requirements on  Junos devices: netconf  

Playbooks:  
- **pb.bgp.yml**: It load a configuration file to Junos devices from the jinja 2 template **bgp.j2** that is automatically rendered (the same task renders the jinja2 template with BGP details and loads it to Junos devices).  
Another task in the same playbook audit the BGP status of Junos devices (checking if the new BGP neighbors are established, and checking if the Junos devices learnt some routes wuth BGP. For more details about these check with the **junos_command** module and its optional **waitfor** argument, please visit https://github.com/ksator/ansible-training-for-junos/tree/master/junos_command).  
- **pb.bgp.2.yml**: it does the same thing as **pb.bgp.yml** but we splitted into two separate tasks the template rendering (so we can have a local copy of the document) and the configuration loading. Also **pb.bgp.2.yml** runs more tests than **pb.bgp.yml* 
- **pb.change_dns_servers.yml**: it uses the template **change-dns-servers.j2** and the variables **change-dns-servers.yml** to reconfigure the list of DNS servers on Junos Devices (adding some and removing others). It retrieves the new configuration. 

Usage:
```
ansible-playbook junos_template/pb.bgp.yml --limit ex4300-4 --tags "configuration" --check --diff  
ansible-playbook junos_template/pb.bgp.yml  
ansible-playbook rollback/pb.yml

ansible-playbook junos_template/pb.bgp.2.yml  
ls junos_template/render/   
more junos_template/render/ex4300-10.conf
ansible-playbook rollback/pb.yml

ansible-playbook junos_template/pb.change_dns_servers.yml --check --diff --limit ex4300-4
ansible-playbook junos_template/pb.change_dns_servers.yml
ls junos_template/   
more junos_template/get_config.log
more junos_template/ex4300-10.conf
ansible-playbook rollback/pb.yml

```

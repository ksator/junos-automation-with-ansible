Module: shell
Executes commands
Documentation : http://docs.ansible.com/ansible/shell_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  
- **pb.git.yml**: use the ansible module **template** to create the junos configuration for new devices based on the template **initial_configuration.j2**. The junos configuration files created are stored in the local directory. Nothing is loaded on Junos devices.Then the rendered configuration are pushed to the remote git repository.


Usage:   
```
ansible-playbook shell/pb.git.yml
```

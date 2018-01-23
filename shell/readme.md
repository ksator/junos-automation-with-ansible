Module: shell
Executes commands
Documentation : http://docs.ansible.com/ansible/shell_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  
- **pb_git.yml**: it uses the ansible module **template** to create the junos configuration for junos devices based on the template **initial_configuration.j2**. The junos configuration files created are stored in the local directory. Nothing is loaded on Junos devices. Then the rendered configuration files are pushed to the remote git repository.


Usage:   
```
ansible-playbook shell/pb_git.yml --extra-var comment="git push from ansible playbook shell/pb_git.yml"
```

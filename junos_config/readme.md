Module: junos_config  
Manages configuration on Junos devices (rollback, zeroize, set/delete commands)   
Documentation: http://docs.ansible.com/ansible/junos_config_module.html  
source code: https://github.com/ansible/ansible-modules-core/tree/devel/network/junos   
Installation: this is a core module. It ships with ansible itself     
Requirements on Ansible: Ansible 2.1 and junos-eznc    
Requirements on  Junos devices: netconf  

Playbooks:  
- pb.vlans.yml: configure a list of vlans on Junos devices and double check on Junos devices if it is OK with the new operationnal state.   
- pb.rollback.yml: rollback junos configuration on devices  (rollback 3)  
- pb.yml: pass some set/delete commands to Junos devices.   

Usage:  
```
ansible-playbook junos_config/pb.vlans.yml --diff
ansible-playbook junos_config/pb.rollback.yml

ansible-playbook junos_config/pb.yml --check --diff --limit 172.30.179.111
ansible-playbook junos_config/pb.yml --check 
ansible-playbook junos_config/pb.yml

```

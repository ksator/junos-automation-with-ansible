Module: wait_for  
Documentation: http://docs.ansible.com/ansible/wait_for_module.html  
Installation: this is a core module. It ships with ansible itself.       

Playbooks: 
- pb.yml: It checks if the port 830 (this is the default netconf port) is open on Junos devices.  

Usage: 
```
ansible-playbook wait_for/pb.yml  
```

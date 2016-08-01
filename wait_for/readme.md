Module: wait_for  
wait for a set amount of time for a port to become available  
Documentation: http://docs.ansible.com/ansible/wait_for_module.html  
Installation: this is a core module. It ships with ansible itself.       

Playbooks: 
- **pb.yml**: checks if the port 830 (this is the default netconf port) and 22 (default SSH port) are open on Junos devices. checks if the port 3000 (this is the default rest port on Junos) is open on MX.    

Usage: 
```
ansible-playbook wait_for/pb.yml  
```

Module: uri   
Documenatation: http://docs.ansible.com/ansible/uri_module.html  
Installation: this is a core module. It ships with ansible itself.   
Dependency: The dependency on httplib2 was removed in Ansible 2.1  
Requirement: Enable rest api on junos (default port is 3000)   
```
set system services rest http
```

Playbook: 
- pb.yml: it makes a rest call to a junos devices, and use the debug module to print some of the collected data.   

Usage: 
```
ansible-playbook uri/pb.yml
```

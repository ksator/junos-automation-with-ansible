Module: uri   
Documenatation: http://docs.ansible.com/ansible/uri_module.html  
Installation: this is a core module. It ships with ansible itself.   
Dependency: The dependency on httplib2 was removed in Ansible 2.1  
Requirement on Junos: Enable rest api (default port is 3000)   
```
set system services rest http
```

Playbook: 
- **pb.yml**: it check if the rest api default port (3000) is enabled on the MX device. it makes a rest call to the junos devices. It saves locally the downloaded file.  it uses the debug module to print some of the collected data.   

Usage: 
```
ansible-playbook uri/pb.yml
ls  uri/
more uri/somelog.json

```

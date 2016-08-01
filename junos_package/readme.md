
Module: junos_package  
Installs packages on remote devices running Junos.  Compare the package version with the one running on the remote device and install the specified version if there is a mismatch. You can run it in check mode.  
Documentation: http://docs.ansible.com/ansible/junos_package_module.html  
Installation: this is a core module. It ships with ansible itself   
Requirements on Ansible: Ansible 2.1 and junos-eznc  
Requirements on  Junos devices: netconf  

Playbooks:  
- **pb.yml**: upgrade a Junos device. 

Usage:
```
ansible-playbook junos_package/pb.yml --check
ansible-playbook junos_package/pb.yml
```






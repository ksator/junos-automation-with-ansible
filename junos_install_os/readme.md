module: junos_install_os  
Install a Junos OS image. if the existing Junos OS version matches the desired version, no action is performed. you can run it in check mode  
doc: http://junos-ansible-modules.readthedocs.io/en/1.3.1/  
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download the junos role to the Ansible server, execute the command: ansible-galaxy install Juniper.junos  
requirements: enable netconf on junos. py-junos-eznc on Ansible.    

playbook: 
- pb.yml: upgrade Junos devices  

usage:  
```
ansible-playbook junos_install_os/pb.yml  --check
ansible-playbook junos_install_os/pb.yml  
```

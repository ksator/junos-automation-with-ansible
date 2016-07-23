lookup allows Ansible to access data from outside sources (files ...)  
Doc: http://docs.ansible.com/ansible/playbooks_lookups.html  

playbook: 
- pb.yml: this pb uses various lookups to get the current time from the Ansible server, and print the time using tge debug module.    

usage: 
```
sudo ansible-playbook lookup/pb.yml   
```

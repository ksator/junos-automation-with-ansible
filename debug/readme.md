module: debug  
installation: it is a core module  
doc: http://docs.ansible.com/ansible/debug_module.html  
useful for debugging. you can use it together with ‘when:’ (http://docs.ansible.com/ansible/playbooks_conditionals.html#the-when-statement)  
playbook: this pb get the junos facts, and print the hostname of the devices if they are not running a specific junos version.     
usage: sudo ansible-playbook debug/pb.yml   

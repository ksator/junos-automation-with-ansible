module: ping  
http://docs.ansible.com/ansible/ping_module.html  
This is not an ICMP ping: it tries to connect to host, and it verifies there is a usable python on the remote host, and it returns a pong on success  
Ths is a core module  


the module is ping, the username is administrator, the endpoint is an ubuntu vm (172.30.204.10):
```
ansible --help

ansible 172.30.204.10 -m ping -u administrator -k
SSH password:
172.30.204.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}


ansible 172.30.204.10 -m ping -u administrator --ask-pass
SSH password: 
172.30.204.10 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

you can also use the command core module to test: https://github.com/ksator/ansible-training-for-junos/tree/master/command  


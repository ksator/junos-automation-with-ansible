module: ping  
http://docs.ansible.com/ansible/ping_module.html  
This is not an ICMP ping: it connects to an host, and it verifies if it can use python on the remote host, and it returns a pong on success  
Ths is a core module  


the module is ```ping```, the username is ```administrator```, the endpoint is the ubuntu vm ```172.30.204.10```:
```
ansible --help
```
```
ansible 172.30.204.10 -m ping -u administrator -k
SSH password:
172.30.204.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
```
ansible 172.30.204.10 -m ping -u administrator --ask-pass
SSH password: 
172.30.204.10 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```


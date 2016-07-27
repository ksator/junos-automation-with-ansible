http://docs.ansible.com/ansible/ping_module.html  
Ths is a core module  
This is not an ICMP ping.   
Try to connect to host, verify there is a usable python and return pong on success  

```
$ ansible vm -m ping -u administrator -k
SSH password: 
172.30.204.10 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
$ ansible vm -m ping -u administrator --ask-pass
SSH password: 
172.30.204.10 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
$
```

you can use the ansible ping module for testing: https://github.com/ksator/ansible-training-for-junos/ping/readme.md  

Another Ansible module that is useful for testing is the command module.    
this is a core module: http://docs.ansible.com/ansible/command_module.html   
It runs custom commands on the host and returns the results.  
To run the command command using echo, a Unix command that echoes a string to the terminal, enter the following command.  

```
$ ansible vm -m command -a "/bin/echo hello" -u administrator --ask-pass
SSH password: 
172.30.204.10 | SUCCESS | rc=0 >>
hello
```


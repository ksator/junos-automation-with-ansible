you can use the ansible ping module for testing: https://github.com/ksator/ansible-training-for-junos/tree/master/command  

Another Ansible module that is useful for testing is the command module.    
module: command
this is a core module 
doc: http://docs.ansible.com/ansible/command_module.html   
It runs custom commands on the host and returns the results.  

To run the command command using echo, a Unix command that echoes a string to the terminal, enter the following command.  
The module is command, the module argument is /bin/echo hello, the host is vm, the remote user is administrator.

```
$ ansible --help
$ ansible vm -m command -a "/bin/echo hello" -u administrator --ask-pass
SSH password: 
172.30.204.10 | SUCCESS | rc=0 >>
hello
```


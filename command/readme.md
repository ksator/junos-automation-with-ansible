you can use the ansible ping module for testing: https://github.com/ksator/ansible-training-for-junos/tree/master/ping  
Another Ansible module that is useful for testing is the command module.    

module: command  
this is a core module   
doc: http://docs.ansible.com/ansible/command_module.html   
It runs custom commands on the host and returns the results.  

To run the command command using echo, a Unix command that echoes a string to the terminal, enter the following command.  
The module is``` command```, the module argument is ```/bin/echo hello```, the endpoint is ```172.30.204.10``` (an ubuntu vm), the remote user is ```administrator```.

```
ansible --help
```
```
# more hosts | grep 172.30.204.10
172.30.204.10
```
```
# ansible 172.30.204.10 -m command -a "/bin/echo hello" -u administrator --ask-pass
SSH password: 
172.30.204.10 | SUCCESS | rc=0 >>
hello
```

About response code:  
```
# ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=128 time=20.0 ms
^C
--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 20.093/20.093/20.093/0.000 ms

# echo $?
0
```
```
# ping 1.2.3.4
PING 1.2.3.4 (1.2.3.4) 56(84) bytes of data.
^C
--- 1.2.3.4 ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1007ms

# echo $?
1
```
Using response code with a playbook:
```
# ansible-playbook command/pb.yml --ask-pass
SSH password: 

PLAY [run commands and print response codes] *****************************************************************************************************************************

TASK [run a command that is going to succeed] ****************************************************************************************************************************
changed: [172.30.204.10]

TASK [print echo $?] *****************************************************************************************************************************************************
ok: [172.30.204.10] => {
    "msg": "response code is 0"
}

TASK [run a command that is going to fail] *******************************************************************************************************************************
fatal: [172.30.204.10]: FAILED! => {"changed": true, "cmd": ["ping", "8.8.8.1", "-c", "2"], "delta": "0:00:11.009356", "end": "2018-01-30 17:02:43.121141", "msg": "non-zero return code", "rc": 1, "start": "2018-01-30 17:02:32.111785", "stderr": "", "stderr_lines": [], "stdout": "PING 8.8.8.1 (8.8.8.1) 56(84) bytes of data.\n\n--- 8.8.8.1 ping statistics ---\n2 packets transmitted, 0 received, 100% packet loss, time 1006ms", "stdout_lines": ["PING 8.8.8.1 (8.8.8.1) 56(84) bytes of data.", "", "--- 8.8.8.1 ping statistics ---", "2 packets transmitted, 0 received, 100% packet loss, time 1006ms"]}
...ignoring

TASK [print echo $?] *****************************************************************************************************************************************************
ok: [172.30.204.10] => {
    "msg": "response code is 1"
}

PLAY RECAP ***************************************************************************************************************************************************************
172.30.204.10              : ok=4    changed=2    unreachable=0    failed=0   

root@ubuntu:~/ansible-training-for-junos-automation# 


```

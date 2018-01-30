Module: junos_rollback  
Rollback the configuration of a device running Junos  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.4.3/   
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).   
To download and install it to the Ansible server, execute the command: ```ansible-galaxy install Juniper.junos,1.4.3```  

Playbooks: 
- pb.yml: it rollbacks Junos configuration on junos devices. The rollback id is a variable. This variable is not defined. so you need to pass it as an ```extra-var```.     

Usage: 
```
# ls junos_rollback
pb.yml  readme.md
```
```
# ansible-playbook junos_rollback/pb.yml --extra-var rbid=1

PLAY [Rollback configuration on junos devices] ***************************************************************************************************************************

TASK [Rollback junos config task] ****************************************************************************************************************************************
changed: [ex4200-7]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   
```
```
# ls junos_rollback
ex4200-7.diff  pb.yml  readme.md  rollback.log
```
```
# more junos_rollback/ex4200-7.diff 

[edit system]
-  host-name ex4200-7;
+  host-name newname;
```
```
# ssh pytraining@172.30.179.107
new_banner
pytraining@172.30.179.107's password: 
--- JUNOS 12.3R11.2 built 2015-09-24 11:15:41 UTC
{master:0}
pytraining@newname> show system commit 
0   2018-01-23 12:34:30 CET by pytraining via netconf
    configuration rolled back by Ansible using rbid 1
1   2018-01-23 12:33:41 CET by pytraining via cli
                                        
```
```
{master:0}
pytraining@newname> show configuration | compare rollback 1 
[edit system]
-  host-name ex4200-7;
+  host-name newname;

{master:0}
pytraining@newname> exit 

Connection to 172.30.179.107 closed.
```

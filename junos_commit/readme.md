Module: junos_commit  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.4.3/  
The use case is to confirm a previous commit confirm (before the automatic rollback).    
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).   
To download and install it to the Ansible server, execute the command: ```ansible-galaxy install Juniper.junos,1.4.3```  
Requirement on Junos devices: enable netconf.  
Requirements on Ansible: junos-eznc  

playbooks: 
- **pb.yml**: Execute a commit on a group of Junos devices independently of loading a configuration. 

Usage: 
```
# ssh pytraining@172.30.179.107
pytraining@172.30.179.107's password: 
--- JUNOS 12.3R11.2 built 2015-09-24 11:15:41 UTC
{master:0}
pytraining@ex4200-7> edit 
Entering configuration mode

{master:0}[edit]
pytraining@ex4200-7# set system host-name newname     
pytraining@ex4200-7# commit confirmed     
configuration check succeeds
commit confirmed will be automatically rolled back in 10 minutes unless confirmed
commit complete

# commit confirmed will be rolled back in 10 minutes
{master:0}[edit]
pytraining@newname# exit 
Exiting configuration mode

# commit confirmed will be rolled back in 10 minutes
{master:0}
```
```
pytraining@newname> show system commit 
0   2018-01-23 11:41:11 CET by pytraining via cli commit confirmed, rollback in 10mins
```

```
# ansible-playbook junos_commit/pb.yml 

PLAY [junos_commit] ******************************************************************************************************************************************************

TASK [confirm a commit confirm] ******************************************************************************************************************************************
changed: [ex4200-7]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   
```
```
# ssh pytraining@172.30.179.107
pytraining@172.30.179.107's password: 
--- JUNOS 12.3R11.2 built 2015-09-24 11:15:41 UTC
{master:0}
pytraining@newname> show system commit 
0   2018-01-23 11:41:40 CET by pytraining via netconf
    confirm a commit confirm
1   2018-01-23 11:41:11 CET by pytraining via cli commit confirmed, rollback in 10mins
```                                        


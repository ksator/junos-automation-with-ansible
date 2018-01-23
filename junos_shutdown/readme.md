Module: junos_shutdown  
Shut down or reboot a device running Junos OS.  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.4.3/
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).   
To download and install it to the Ansible server, execute the command ```sudo ansible-galaxy install Juniper.junos,1.4.3```  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos. 


Playbooks:  
- **pb.yml**: this playbook reboots a Junos device

Usage:  
```
# ansible-playbook junos_shutdown/pb.yml 
Device password: 

PLAY [reboot Junos devices] **********************************************************************************************************************************************

TASK [junos_shutdown_task] ***********************************************************************************************************************************************
changed: [ex4200-7]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   

```
```
# ssh pytraining@172.30.179.107
pytraining@172.30.179.107's password: 
--- JUNOS 12.3R11.2 built 2015-09-24 11:15:41 UTC
{master:0}
pytraining@newname> show system uptime 
fpc0:
--------------------------------------------------------------------------
Current time: 2018-01-23 17:49:41 CET
System booted: 2018-01-23 17:47:05 CET (00:02:36 ago)
Protocols started: 2018-01-23 17:49:13 CET (00:00:28 ago)
Last configured: 2018-01-23 15:56:39 CET (01:53:02 ago) by pytraining
 5:49PM  up 3 mins, 1 user, load averages: 2.88, 1.06, 0.42

{master:0}
pytraining@newname> 

```

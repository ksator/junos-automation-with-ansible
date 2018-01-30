Module: slack  
it send slack notifications.  
Documenatation: http://docs.ansible.com/ansible/slack_module.html  
Installation: It ships with ansible itself.   

Playbook: 
- **pb.yml**: it configures a junos device and then it sends a slack notification.

Usage: 
```
# ssh pytraining@172.30.179.107
banner
pytraining@172.30.179.107's password: 
--- JUNOS 12.3R11.2 built 2015-09-24 11:15:41 UTC
{master:0}
pytraining@ex4200-7> show configuration system host-name 
host-name ex4200-7;

{master:0}
pytraining@ex4200-7> show configuration system login message 
message banner;

```
```
# ansible-playbook slack/pb.yml --diff

PLAY [pass junos set commands and then send a slack notification] *****************************************************************************************************************

TASK [pass set and delete commands] ***********************************************************************************************************************************************
[edit system]
-  host-name ex4200-7;
+  host-name newname;
[edit system login]
-   message banner;
changed: [ex4200-7]

TASK [Send Slack notification to the team] ****************************************************************************************************************************************
ok: [ex4200-7 -> localhost]

PLAY RECAP ************************************************************************************************************************************************************************
ex4200-7                   : ok=2    changed=1    unreachable=0    failed=0   

```
```
pytraining@newname> show system commit 
0   2018-01-23 15:56:39 CET by pytraining via netconf
    lines configured by Ansible module junos_config

```
```
pytraining@newname> show configuration | compare rollback 1 
[edit system]
-  host-name ex4200-7;
+  host-name newname;
[edit system login]
-   message banner;

```
Here's the slack notification sent by this playbook: ![slack_notification_from_ansible.png](slack_notification.png)  

Module: wait_for  
wait for a set amount of time for a port to become available  
Documentation: http://docs.ansible.com/ansible/wait_for_module.html  
Installation: this is a core module. It ships with ansible itself.       

Playbooks: 
- **pb.yml**: checks if the port 830 (this is the default netconf port) and 22 (default SSH port) on EX are reachable. checks if the port 3000 (this is the default rest port on Junos) is reachable on QFX.    

Usage: 
```
# ansible-playbook wait_for/pb.yml 

PLAY [check ssh and netconf ports on Junos devices] *******************************************************************************************************************************

TASK [Check ssh and netconf ports connectivity] ***********************************************************************************************************************************
ok: [ex4200-12] => (item=22)
ok: [ex4200-7] => (item=22)
ok: [ex4300-18] => (item=22)
ok: [ex4300-9] => (item=22)
ok: [ex4200-8] => (item=22)
ok: [ex4200-12] => (item=830)
ok: [ex4200-7] => (item=830)
ok: [ex4300-9] => (item=830)
ok: [ex4300-18] => (item=830)
ok: [ex4200-8] => (item=830)
ok: [ex4300-17] => (item=22)
ok: [ex4300-17] => (item=830)

PLAY [check rest port on Junos devices] *******************************************************************************************************************************************

TASK [Check REST port connectivity] ***********************************************************************************************************************************************
ok: [qfx5100-44] => (item=3000)

PLAY RECAP ************************************************************************************************************************************************************************
ex4200-12                  : ok=1    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=0    unreachable=0    failed=0   
ex4300-17                  : ok=1    changed=0    unreachable=0    failed=0   
ex4300-18                  : ok=1    changed=0    unreachable=0    failed=0   
ex4300-9                   : ok=1    changed=0    unreachable=0    failed=0   
qfx5100-44                 : ok=1    changed=0    unreachable=0    failed=0   

```

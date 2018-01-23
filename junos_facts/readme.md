Module: junos_facts  
Collect facts from Junos devices. The configuration can be collected as well.  
Documentation: http://docs.ansible.com/ansible/junos_facts_module.html  
source code: https://github.com/ansible/ansible/tree/devel/lib/ansible/modules/network/junos  
Installation: this is a core module. It ships with ansible itself   
Requirements on Ansible: Ansible 2.1 and junos-eznc   
Requirements on  Junos devices: netconf  

Playbooks:  
- **pb_collect_facts.yml **: collect and parse facts.
- **pb_collect_configuration.yml **: collect and save junos configuration in json, xml, set and text formats.    


Usage:  
# pb_collect_facts.yml 

```
# ansible-playbook junos_facts/pb_collect_facts.yml 

PLAY [Get Facts] *********************************************************************************************************************************************************

TASK [Retrieve information from devices running Junos] *******************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-8]
ok: [ex4300-18]
ok: [ex4300-9]
ok: [ex4200-7]
ok: [ex4300-17]
ok: [qfx5100-44]

TASK [Print some facts] **************************************************************************************************************************************************
ok: [ex4200-7] => {
    "msg": "device newname is a ex4200-48t running junos version "
}
ok: [ex4200-8] => {
    "msg": "device ex4200-8 is a ex4200-48t running junos version "
}
ok: [ex4200-12] => {
    "msg": "device ex4200-12 is a ex4200-24t running junos version 15.1R2.9"
}
ok: [ex4300-9] => {
    "msg": "device ex4300-9 is a ex4300-24t running junos version 15.1R5.5"
}
ok: [ex4300-18] => {
    "msg": "device ex4300-18 is a ex4300-24t running junos version 15.1R5.5"
}
ok: [ex4300-17] => {
    "msg": "device ex4300-17 is a ex4300-24t running junos version 15.1R5.5"
}
ok: [qfx5100-44] => {
    "msg": "device qfx5100-44 is a qfx5100-48t-6q running junos version 17.3R1.10"
}

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=2    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=2    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=2    changed=0    unreachable=0    failed=0   
ex4300-17                  : ok=2    changed=0    unreachable=0    failed=0   
ex4300-18                  : ok=2    changed=0    unreachable=0    failed=0   
ex4300-9                   : ok=2    changed=0    unreachable=0    failed=0   
qfx5100-44                 : ok=2    changed=0    unreachable=0    failed=0   
```
# pb_collect_configuration.yml 

```
# ansible-playbook junos_facts/pb_collect_configuration.yml 

PLAY [create configuration_backup directories] ***************************************************************************************************************************

TASK [create configuration directory] ************************************************************************************************************************************
changed: [localhost]

TASK [create configuration subdirectories] *******************************************************************************************************************************
changed: [localhost] => (item=text)
changed: [localhost] => (item=xml)
changed: [localhost] => (item=json)
changed: [localhost] => (item=set)

PLAY [Collect configuration from devices] ********************************************************************************************************************************

TASK [Collect configuration in text format from devices] *****************************************************************************************************************
ok: [ex4200-12]
ok: [ex4300-9]
ok: [ex4300-18]
ok: [ex4200-7]
ok: [ex4200-8]
ok: [qfx5100-44]
ok: [ex4300-17]

TASK [copy collected configuration in configuration/text directory] ******************************************************************************************************
changed: [ex4200-8]
changed: [ex4300-18]
changed: [ex4300-9]
changed: [ex4200-7]
changed: [ex4200-12]
changed: [qfx5100-44]
changed: [ex4300-17]

TASK [Collect configuration in set format from devices] ******************************************************************************************************************
ok: [ex4300-9]
ok: [ex4200-12]
ok: [ex4200-8]
ok: [ex4200-7]
ok: [qfx5100-44]
ok: [ex4300-17]
ok: [ex4300-18]

TASK [copy collected configuration in configuration/set directory] *******************************************************************************************************
changed: [ex4200-7]
changed: [ex4200-8]
changed: [ex4300-9]
changed: [ex4300-18]
changed: [ex4200-12]
changed: [ex4300-17]
changed: [qfx5100-44]

TASK [Collect configuration in json format from devices] *****************************************************************************************************************
ok: [ex4200-8]
ok: [ex4200-7]
ok: [ex4200-12]
ok: [ex4300-9]
ok: [ex4300-18]
ok: [qfx5100-44]
ok: [ex4300-17]

TASK [copy collected configuration in configuration/json directory] ******************************************************************************************************
changed: [ex4200-7]
changed: [ex4200-8]
changed: [ex4200-12]
changed: [ex4300-18]
changed: [ex4300-9]
changed: [qfx5100-44]
changed: [ex4300-17]

TASK [Collect configuration in xml format from devices] ******************************************************************************************************************
ok: [ex4200-12]
ok: [ex4300-18]
ok: [ex4300-9]
ok: [ex4200-8]
ok: [ex4200-7]
ok: [qfx5100-44]
ok: [ex4300-17]

TASK [copy collected configuration in configuration/xml directory] *******************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-7]
changed: [ex4200-8]
changed: [ex4300-9]
changed: [ex4300-18]
changed: [ex4300-17]
changed: [qfx5100-44]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=8    changed=4    unreachable=0    failed=0   
ex4200-7                   : ok=8    changed=4    unreachable=0    failed=0   
ex4200-8                   : ok=8    changed=4    unreachable=0    failed=0   
ex4300-17                  : ok=8    changed=4    unreachable=0    failed=0   
ex4300-18                  : ok=8    changed=4    unreachable=0    failed=0   
ex4300-9                   : ok=8    changed=4    unreachable=0    failed=0   
localhost                  : ok=2    changed=2    unreachable=0    failed=0   
qfx5100-44                 : ok=8    changed=4    unreachable=0    failed=0   
```
```
# ls junos_facts/configuration/
json  set  text  xml
```
```
# ls junos_facts/configuration/xml/
ex4200-12.xml  ex4200-7.xml  ex4200-8.xml  ex4300-17.xml  ex4300-18.xml  ex4300-9.xml  qfx5100-44.xml

```

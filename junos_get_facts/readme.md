module: junos_get_facts  
doc: http://junos-ansible-modules.readthedocs.io/en/1.4.3/  
Retrieve facts for a device running Junos OS, which includes information such as the serial number, product model, Junos OS version ...  
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).  
To download and install this junos role to the Ansible server, execute the command: ```ansible-galaxy install Juniper.junos,1.4.3```  

playbooks: 
- **pb.yml**: get some facts from junos devices.  Save them locally in the directory **inventory**. Print devices hostname if they are not running 12.3R11.2

usage: 
```
# ls junos_get_facts/inventory/
```
```
# ansible-playbook junos_get_facts/pb.yml 

PLAY [create inventory directory] ****************************************************************************************************************************************

TASK [create inventory directory] ****************************************************************************************************************************************
ok: [localhost]

PLAY [Get Facts] *********************************************************************************************************************************************************

TASK [remove host from inventory directory] ******************************************************************************************************************************
ok: [ex4200-8]
ok: [ex4200-12]
ok: [ex4200-7]

TASK [Retrieve information from devices running Junos] *******************************************************************************************************************
ok: [ex4200-7]
ok: [ex4200-8]
ok: [ex4200-12]

TASK [Print some facts] **************************************************************************************************************************************************
skipping: [ex4200-7]
skipping: [ex4200-8]
ok: [ex4200-12] => {
    "msg": "device ex4200-12 runs version 15.1R2.9"
}

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=3    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=2    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=2    changed=0    unreachable=0    failed=0   
localhost                  : ok=1    changed=0    unreachable=0    failed=0   
```
```
# ls junos_get_facts/inventory/
ex4200-12-facts.json  ex4200-8-facts.json  newname-facts.json
```
```
# more junos_get_facts/inventory/ex4200-12-facts.json 
{"domain": "poc-nl.jnpr.net", "hostname_info": {"fpc0": "ex4200-12"}, "version_RE1": null, "version_RE0": null, "re_master": {"default": "0"}, "serialnumber": "BM02101180
07", "vc_master": "0", "RE_hw_mi": false, "HOME": "/var/home/remote", "master_state": true, "re_info": {"default": {"default": {"status": "OK", "last_reboot_reason": "0x2
:watchdog", "model": "EX4200-24T, 8 POE", "mastership_state": "master"}, "0": {"status": "OK", "last_reboot_reason": "0x2:watchdog", "model": "EX4200-24T, 8 POE", "master
ship_state": "master"}}}, "srx_cluster_id": null, "hostname": "ex4200-12", "virtual": false, "version": "15.1R2.9", "master": "RE0", "vc_fabric": false, "personality": "S
WITCH", "srx_cluster_redundancy_group": null, "version_info": {"major": [15, 1], "type": "R", "build": 9, "minor": "2"}, "re_name": "fpc0", "srx_cluster": null, "vc_mode"
: "Enabled", "vc_capable": true, "ifd_style": "SWITCH", "model_info": {"fpc0": "EX4200-24T"}, "RE0": {"status": "OK", "last_reboot_reason": "0x2:watchdog", "model": "EX42
00-24T, 8 POE", "up_time": "85 days, 5 hours, 13 seconds", "mastership_state": "master"}, "RE1": null, "fqdn": "ex4200-12.poc-nl.jnpr.net", "junos_info": {"fpc0": {"text"
: "15.1R2.9", "object": {"major": [15, 1], "type": "R", "build": 9, "minor": "2"}}}, "has_2RE": false, "switch_style": "VLAN", "model": "EX4200-24T", "current_re": ["mast
er", "node", "fwdd", "member", "pfem", "fpc0", "feb0", "fpc16"]}

```

Module: debug  
Doc: http://docs.ansible.com/ansible/debug_module.html  
you can use this module to print something during playbook execution. Useful for debugging  
Installation: this is a core module. It ships with ansible itself  

module: junos_get_facts  
doc: http://junos-ansible-modules.readthedocs.io/en/1.4.3/  
Retrieve facts for a device running Junos OS, which includes information such as the serial number, product model, Junos OS version ...   
installation: this role is hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/).   
To download the junos role to the Ansible server, execute the command: ```ansible-galaxy install Juniper.junos,1.4.3```  
requirements on Junos devices: netconf  
requirements on Ansible: junos-eznc. junos-netconify when using the console optional argument.    

Playbooks:  
- **pb.yml**: this playbook get the junos facts from a group of junos devices, and print the hostname of the devices that are not running a specific junos version.     
- **pb.verbose.yml**: this playbook get the junos facts from a group of junos devices, and print the hostname of the devices that are not running a specific junos version. it also print the junos facts if we use -vv     


Usage: 
```
# ansible-playbook debug/pb.yml 

PLAY [Get Facts] *********************************************************************************************************************************************************

TASK [Retrieve information from devices running Junos] *******************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-7]
ok: [ex4200-8]

TASK [Print some facts] **************************************************************************************************************************************************
skipping: [ex4200-7]
skipping: [ex4200-8]
ok: [ex4200-12] => {
    "msg": "device ex4200-12 runs version 15.1R2.9"
}

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=2    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=0    unreachable=0    failed=0   

```

```
# ansible-playbook debug/pb.verbose.yml

PLAY [Get Facts] *********************************************************************************************************************************************************

TASK [Retrieve information from devices running Junos] *******************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-7]
ok: [ex4200-8]

TASK [Print some facts] **************************************************************************************************************************************************
skipping: [ex4200-7]
skipping: [ex4200-8]
ok: [ex4200-12] => {
    "msg": "device ex4200-12 runs version 15.1R2.9"
}

TASK [print devices facts using ansible-playbook command with -vv] *******************************************************************************************************
skipping: [ex4200-7]
skipping: [ex4200-8]
skipping: [ex4200-12]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=2    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=0    unreachable=0    failed=0   

```

```
# ansible-playbook debug/pb.verbose.yml -vv
ansible-playbook 2.4.2.0
  config file = /home/ksator/ansible-training-for-junos-automation/ansible.cfg
  configured module search path = [u'/home/ksator/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python2.7/dist-packages/ansible
  executable location = /usr/local/bin/ansible-playbook
  python version = 2.7.6 (default, Oct 26 2016, 20:30:19) [GCC 4.8.4]
Using /home/ksator/ansible-training-for-junos-automation/ansible.cfg as config file

PLAYBOOK: pb.verbose.yml *************************************************************************************************************************************************
1 plays in debug/pb.verbose.yml

PLAY [Get Facts] *********************************************************************************************************************************************************
META: ran handlers

TASK [Retrieve information from devices running Junos] *******************************************************************************************************************
task path: /home/ksator/ansible-training-for-junos-automation/debug/pb.verbose.yml:11
ok: [ex4200-12] => {"changed": false, "facts": {"HOME": "/var/home/remote", "RE0": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-24T, 8 POE", "status": "OK", "up_time": "85 days, 2 hours, 40 minutes, 42 seconds"}, "RE1": null, "RE_hw_mi": false, "current_re": ["master", "node", "fwdd", "member", "pfem", "fpc0", "feb0", "fpc16"], "domain": "poc-nl.jnpr.net", "fqdn": "ex4200-12.poc-nl.jnpr.net", "has_2RE": false, "hostname": "ex4200-12", "hostname_info": {"fpc0": "ex4200-12"}, "ifd_style": "SWITCH", "junos_info": {"fpc0": {"object": {"build": 9, "major": [15, 1], "minor": "2", "type": "R"}, "text": "15.1R2.9"}}, "master": "RE0", "master_state": true, "model": "EX4200-24T", "model_info": {"fpc0": "EX4200-24T"}, "personality": "SWITCH", "re_info": {"default": {"0": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-24T, 8 POE", "status": "OK"}, "default": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-24T, 8 POE", "status": "OK"}}}, "re_master": {"default": "0"}, "re_name": "fpc0", "serialnumber": "BM0210118007", "srx_cluster": null, "srx_cluster_id": null, "srx_cluster_redundancy_group": null, "switch_style": "VLAN", "vc_capable": true, "vc_fabric": false, "vc_master": "0", "vc_mode": "Enabled", "version": "15.1R2.9", "version_RE0": null, "version_RE1": null, "version_info": {"build": 9, "major": [15, 1], "minor": "2", "type": "R"}, "virtual": false}}
ok: [ex4200-8] => {"changed": false, "facts": {"HOME": "/var/home/remote", "RE0": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-48T, 8 POE", "status": "OK", "up_time": "85 days, 2 hours, 40 minutes, 47 seconds"}, "RE1": null, "RE_hw_mi": false, "current_re": ["master", "node", "fwdd", "member", "pfem", "fpc0", "feb0", "fpc16"], "domain": "poc-nl.jnpr.net", "fqdn": "ex4200-8.poc-nl.jnpr.net", "has_2RE": false, "hostname": "ex4200-8", "hostname_info": {"fpc0": "ex4200-8"}, "ifd_style": "SWITCH", "junos_info": {"fpc0": {"object": {"build": 2, "major": [12, 3], "minor": "11", "type": "R"}, "text": "12.3R11.2"}}, "master": "RE0", "master_state": true, "model": "EX4200-48T", "model_info": {"fpc0": "EX4200-48T"}, "personality": "SWITCH", "re_info": {"default": {"0": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-48T, 8 POE", "status": "OK"}, "default": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-48T, 8 POE", "status": "OK"}}}, "re_master": {"default": "0"}, "re_name": "fpc0", "serialnumber": "BP0208520468", "srx_cluster": null, "srx_cluster_id": null, "srx_cluster_redundancy_group": null, "switch_style": "VLAN", "vc_capable": true, "vc_fabric": false, "vc_master": "0", "vc_mode": "Enabled", "version": "12.3R11.2", "version_RE0": null, "version_RE1": null, "version_info": {"build": 2, "major": [12, 3], "minor": "11", "type": "R"}, "virtual": false}}
ok: [ex4200-7] => {"changed": false, "facts": {"HOME": "/var/home/remote", "RE0": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-48T, 8 POE", "status": "OK", "up_time": "85 days, 2 hours, 40 minutes, 48 seconds"}, "RE1": null, "RE_hw_mi": false, "current_re": ["master", "node", "fwdd", "member", "pfem", "fpc0", "feb0", "fpc16"], "domain": "poc-nl.jnpr.net", "fqdn": "newhostname.poc-nl.jnpr.net", "has_2RE": false, "hostname": "newhostname", "hostname_info": {"fpc0": "newhostname"}, "ifd_style": "SWITCH", "junos_info": {"fpc0": {"object": {"build": 2, "major": [12, 3], "minor": "11", "type": "R"}, "text": "12.3R11.2"}}, "master": "RE0", "master_state": true, "model": "EX4200-48T", "model_info": {"fpc0": "EX4200-48T"}, "personality": "SWITCH", "re_info": {"default": {"0": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-48T, 8 POE", "status": "OK"}, "default": {"last_reboot_reason": "0x2:watchdog", "mastership_state": "master", "model": "EX4200-48T, 8 POE", "status": "OK"}}}, "re_master": {"default": "0"}, "re_name": "fpc0", "serialnumber": "BP0208111225", "srx_cluster": null, "srx_cluster_id": null, "srx_cluster_redundancy_group": null, "switch_style": "VLAN", "vc_capable": true, "vc_fabric": false, "vc_master": "0", "vc_mode": "Mixed", "version": "12.3R11.2", "version_RE0": null, "version_RE1": null, "version_info": {"build": 2, "major": [12, 3], "minor": "11", "type": "R"}, "virtual": false}}

TASK [Print some facts] **************************************************************************************************************************************************
task path: /home/ksator/ansible-training-for-junos-automation/debug/pb.verbose.yml:18
skipping: [ex4200-7] => {"changed": false, "skip_reason": "Conditional result was False"}
skipping: [ex4200-8] => {"changed": false, "skip_reason": "Conditional result was False"}
ok: [ex4200-12] => {
    "msg": "device ex4200-12 runs version 15.1R2.9"
}

TASK [print devices facts using ansible-playbook command with -vv] *******************************************************************************************************
task path: /home/ksator/ansible-training-for-junos-automation/debug/pb.verbose.yml:23
ok: [ex4200-7] => {
    "msg": {
        "changed": false, 
        "facts": {
            "HOME": "/var/home/remote", 
            "RE0": {
                "last_reboot_reason": "0x2:watchdog", 
                "mastership_state": "master", 
                "model": "EX4200-48T, 8 POE", 
                "status": "OK", 
                "up_time": "85 days, 2 hours, 40 minutes, 48 seconds"
            }, 
            "RE1": null, 
            "RE_hw_mi": false, 
            "current_re": [
                "master", 
                "node", 
                "fwdd", 
                "member", 
                "pfem", 
                "fpc0", 
                "feb0", 
                "fpc16"
            ], 
            "domain": "poc-nl.jnpr.net", 
            "fqdn": "newhostname.poc-nl.jnpr.net", 
            "has_2RE": false, 
            "hostname": "newhostname", 
            "hostname_info": {
                "fpc0": "newhostname"
            }, 
            "ifd_style": "SWITCH", 
            "junos_info": {
                "fpc0": {
                    "object": {
                        "build": 2, 
                        "major": [
                            12, 
                            3
                        ], 
                        "minor": "11", 
                        "type": "R"
                    }, 
                    "text": "12.3R11.2"
                }
            }, 
            "master": "RE0", 
            "master_state": true, 
            "model": "EX4200-48T", 
            "model_info": {
                "fpc0": "EX4200-48T"
            }, 
            "personality": "SWITCH", 
            "re_info": {
                "default": {
                    "0": {
                        "last_reboot_reason": "0x2:watchdog", 
                        "mastership_state": "master", 
                        "model": "EX4200-48T, 8 POE", 
                        "status": "OK"
                    }, 
                    "default": {
                        "last_reboot_reason": "0x2:watchdog", 
                        "mastership_state": "master", 
                        "model": "EX4200-48T, 8 POE", 
                        "status": "OK"
                    }
                }
            }, 
            "re_master": {
                "default": "0"
            }, 
            "re_name": "fpc0", 
            "serialnumber": "BP0208111225", 
            "srx_cluster": null, 
            "srx_cluster_id": null, 
            "srx_cluster_redundancy_group": null, 
            "switch_style": "VLAN", 
            "vc_capable": true, 
            "vc_fabric": false, 
            "vc_master": "0", 
            "vc_mode": "Mixed", 
            "version": "12.3R11.2", 
            "version_RE0": null, 
            "version_RE1": null, 
            "version_info": {
                "build": 2, 
                "major": [
                    12, 
                    3
                ], 
                "minor": "11", 
                "type": "R"
            }, 
            "virtual": false
        }, 
        "failed": false
    }
}
ok: [ex4200-8] => {
    "msg": {
        "changed": false, 
        "facts": {
            "HOME": "/var/home/remote", 
            "RE0": {
                "last_reboot_reason": "0x2:watchdog", 
                "mastership_state": "master", 
                "model": "EX4200-48T, 8 POE", 
                "status": "OK", 
                "up_time": "85 days, 2 hours, 40 minutes, 47 seconds"
            }, 
            "RE1": null, 
            "RE_hw_mi": false, 
            "current_re": [
                "master", 
                "node", 
                "fwdd", 
                "member", 
                "pfem", 
                "fpc0", 
                "feb0", 
                "fpc16"
            ], 
            "domain": "poc-nl.jnpr.net", 
            "fqdn": "ex4200-8.poc-nl.jnpr.net", 
            "has_2RE": false, 
            "hostname": "ex4200-8", 
            "hostname_info": {
                "fpc0": "ex4200-8"
            }, 
            "ifd_style": "SWITCH", 
            "junos_info": {
                "fpc0": {
                    "object": {
                        "build": 2, 
                        "major": [
                            12, 
                            3
                        ], 
                        "minor": "11", 
                        "type": "R"
                    }, 
                    "text": "12.3R11.2"
                }
            }, 
            "master": "RE0", 
            "master_state": true, 
            "model": "EX4200-48T", 
            "model_info": {
                "fpc0": "EX4200-48T"
            }, 
            "personality": "SWITCH", 
            "re_info": {
                "default": {
                    "0": {
                        "last_reboot_reason": "0x2:watchdog", 
                        "mastership_state": "master", 
                        "model": "EX4200-48T, 8 POE", 
                        "status": "OK"
                    }, 
                    "default": {
                        "last_reboot_reason": "0x2:watchdog", 
                        "mastership_state": "master", 
                        "model": "EX4200-48T, 8 POE", 
                        "status": "OK"
                    }
                }
            }, 
            "re_master": {
                "default": "0"
            }, 
            "re_name": "fpc0", 
            "serialnumber": "BP0208520468", 
            "srx_cluster": null, 
            "srx_cluster_id": null, 
            "srx_cluster_redundancy_group": null, 
            "switch_style": "VLAN", 
            "vc_capable": true, 
            "vc_fabric": false, 
            "vc_master": "0", 
            "vc_mode": "Enabled", 
            "version": "12.3R11.2", 
            "version_RE0": null, 
            "version_RE1": null, 
            "version_info": {
                "build": 2, 
                "major": [
                    12, 
                    3
                ], 
                "minor": "11", 
                "type": "R"
            }, 
            "virtual": false
        }, 
        "failed": false
    }
}
ok: [ex4200-12] => {
    "msg": {
        "changed": false, 
        "facts": {
            "HOME": "/var/home/remote", 
            "RE0": {
                "last_reboot_reason": "0x2:watchdog", 
                "mastership_state": "master", 
                "model": "EX4200-24T, 8 POE", 
                "status": "OK", 
                "up_time": "85 days, 2 hours, 40 minutes, 42 seconds"
            }, 
            "RE1": null, 
            "RE_hw_mi": false, 
            "current_re": [
                "master", 
                "node", 
                "fwdd", 
                "member", 
                "pfem", 
                "fpc0", 
                "feb0", 
                "fpc16"
            ], 
            "domain": "poc-nl.jnpr.net", 
            "fqdn": "ex4200-12.poc-nl.jnpr.net", 
            "has_2RE": false, 
            "hostname": "ex4200-12", 
            "hostname_info": {
                "fpc0": "ex4200-12"
            }, 
            "ifd_style": "SWITCH", 
            "junos_info": {
                "fpc0": {
                    "object": {
                        "build": 9, 
                        "major": [
                            15, 
                            1
                        ], 
                        "minor": "2", 
                        "type": "R"
                    }, 
                    "text": "15.1R2.9"
                }
            }, 
            "master": "RE0", 
            "master_state": true, 
            "model": "EX4200-24T", 
            "model_info": {
                "fpc0": "EX4200-24T"
            }, 
            "personality": "SWITCH", 
            "re_info": {
                "default": {
                    "0": {
                        "last_reboot_reason": "0x2:watchdog", 
                        "mastership_state": "master", 
                        "model": "EX4200-24T, 8 POE", 
                        "status": "OK"
                    }, 
                    "default": {
                        "last_reboot_reason": "0x2:watchdog", 
                        "mastership_state": "master", 
                        "model": "EX4200-24T, 8 POE", 
                        "status": "OK"
                    }
                }
            }, 
            "re_master": {
                "default": "0"
            }, 
            "re_name": "fpc0", 
            "serialnumber": "BM0210118007", 
            "srx_cluster": null, 
            "srx_cluster_id": null, 
            "srx_cluster_redundancy_group": null, 
            "switch_style": "VLAN", 
            "vc_capable": true, 
            "vc_fabric": false, 
            "vc_master": "0", 
            "vc_mode": "Enabled", 
            "version": "15.1R2.9", 
            "version_RE0": null, 
            "version_RE1": null, 
            "version_info": {
                "build": 9, 
                "major": [
                    15, 
                    1
                ], 
                "minor": "2", 
                "type": "R"
            }, 
            "virtual": false
        }, 
        "failed": false
    }
}
META: ran handlers
META: ran handlers

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=3    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=2    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=2    changed=0    unreachable=0    failed=0   

```
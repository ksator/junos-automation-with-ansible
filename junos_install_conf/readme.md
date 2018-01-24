Module: junos_install_config  
Doc: http://junos-ansible-modules.readthedocs.io/en/1.4.3/    
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download and install it to the Ansible server, execute the command ```ansible-galaxy install Juniper.junos,1.4.3```  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  

playbooks:
- **Pb.yml**: install a list of configuration files on junos devices (2 files: syslog.set and banner.set, this makes 2 separate commit, one per file).   
- **pb_bgp_replace.yml**: renders a template, and loads the configuration. uses jsnapy to take snapshots before and after the changes, and compare the snapshots.  

Usage:
# pb.yml

```
# ansible-playbook junos_install_conf/pb.yml --check

PLAY [install conf] ******************************************************************************************************************************************************

TASK [Install configuration to devices running Junos] ********************************************************************************************************************
changed: [ex4200-7] => (item=syslog.set)
changed: [ex4200-7] => (item=banner.set)

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   
```
```
# ansible-playbook junos_install_conf/pb.yml --check --diff

PLAY [install conf] ******************************************************************************************************************************************************

TASK [Install configuration to devices running Junos] ********************************************************************************************************************

[edit system syslog]
     host 192.168.233.20 { ... }
+    host 172.30.18.22 {
+        any notice;
+        authorization info;
+        interactive-commands info;
+    }
changed: [ex4200-7] => (item=syslog.set)

[edit system login]
+   message "this is the new banner";
changed: [ex4200-7] => (item=banner.set)

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   

```
```
# ansible-playbook junos_install_conf/pb.yml

PLAY [install conf] ******************************************************************************************************************************************************

TASK [Install configuration to devices running Junos] ********************************************************************************************************************
changed: [ex4200-7] => (item=syslog.set)
changed: [ex4200-7] => (item=banner.set)

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   

```
```
# more junos_install_conf/ex4200-7_banner.set_2301-161136 

[edit system login]
+   message "this is the new banner";
```
```
# more junos_install_conf/ex4200-7_syslog.set_2301-161121 

[edit system syslog]
     host 192.168.233.20 { ... }
+    host 172.30.18.22 {
+        any notice;
+        authorization info;
+        interactive-commands info;
+    }
```
```
# ssh pytraining@172.30.179.107
this is the new banner
pytraining@172.30.179.107's password: 
--- JUNOS 12.3R11.2 built 2015-09-24 11:15:41 UTC
{master:0}
pytraining@newname> show system commit 
0   2018-01-24 01:11:44 CET by pytraining via netconf
    configured by ansible
1   2018-01-24 01:11:32 CET by pytraining via netconf
    configured by ansible
```
```
pytraining@newname> show configuration | compare rollback 1 
[edit system login]
+   message "this is the new banner";
```
```
pytraining@newname> show configuration | compare rollback 2    
[edit system login]
+   message "this is the new banner";
[edit system syslog]
     host 192.168.233.20 { ... }
+    host 172.30.18.22 {
+        any notice;
+        authorization info;
+        interactive-commands info;
+    }
```
# pb_bgp_replace.yml 

```
# ansible-playbook junos_install_conf/pb_bgp_replace.yml 

PLAY [create a directory] ************************************************************************************************************************************************

TASK [create and push the directory render] ******************************************************************************************************************************
changed: [localhost]

PLAY [create BGP junos configuration] ************************************************************************************************************************************

TASK [Retrieve information from devices running Junos] *******************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-8]
ok: [ex4200-7]

TASK [Print some facts] **************************************************************************************************************************************************
ok: [ex4200-7] => {
    "msg": "device newname is a EX4200-48T running version 12.3R11.2"
}
ok: [ex4200-8] => {
    "msg": "device ex4200-8 is a EX4200-48T running version 12.3R11.2"
}
ok: [ex4200-12] => {
    "msg": "device ex4200-12 is a EX4200-24T running version 15.1R2.9"
}

TASK [Render BGP configuration for junos devices] ************************************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-8]
changed: [ex4200-7]

TASK [Collect Pre Snapshot] **********************************************************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-7]
changed: [ex4200-8]

TASK [Install configuration to devices running Junos] ********************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-7]
ok: [ex4200-8]

TASK [Collect Post Snapshot] *********************************************************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-7]
changed: [ex4200-8]

TASK [check bgp peers states] ********************************************************************************************************************************************
ok: [ex4200-12] => (item={u'peer_loopback': u'192.179.0.107', u'local_ip': u'192.168.10.0', u'peer_ip': u'192.168.10.1', u'interface': u'ge-0/0/0', u'asn': 209, u'name': u'ex4200-7'})
ok: [ex4200-12] => (item={u'peer_loopback': u'192.179.0.108', u'local_ip': u'192.168.10.3', u'peer_ip': u'192.168.10.2', u'interface': u'ge-0/0/1', u'asn': 210, u'name': u'ex4200-8'})
ok: [ex4200-7] => (item={u'peer_loopback': u'192.179.0.108', u'local_ip': u'192.168.10.5', u'peer_ip': u'192.168.10.4', u'interface': u'ge-0/0/1', u'asn': 210, u'name': u'ex4200-8'})
ok: [ex4200-8] => (item={u'peer_loopback': u'192.179.0.107', u'local_ip': u'192.168.10.4', u'peer_ip': u'192.168.10.5', u'interface': u'ge-0/0/0', u'asn': 209, u'name': u'ex4200-7'})
ok: [ex4200-7] => (item={u'peer_loopback': u'192.179.0.112', u'local_ip': u'192.168.10.1', u'peer_ip': u'192.168.10.0', u'interface': u'ge-0/0/0', u'asn': 204, u'name': u'ex4200-12'})
ok: [ex4200-8] => (item={u'peer_loopback': u'192.179.0.112', u'local_ip': u'192.168.10.2', u'peer_ip': u'192.168.10.3', u'interface': u'ge-0/0/1', u'asn': 204, u'name': u'ex4200-12'})

TASK [Compare snapshots] *************************************************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-7]
ok: [ex4200-8]

TASK [Check JSNAPy tests results] ****************************************************************************************************************************************
ok: [ex4200-7] => {
    "changed": false, 
    "msg": "All assertions passed"
}
ok: [ex4200-8] => {
    "changed": false, 
    "msg": "All assertions passed"
}
ok: [ex4200-12] => {
    "changed": false, 
    "msg": "All assertions passed"
}

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=9    changed=3    unreachable=0    failed=0   
ex4200-7                   : ok=9    changed=3    unreachable=0    failed=0   
ex4200-8                   : ok=9    changed=3    unreachable=0    failed=0   
localhost                  : ok=1    changed=1    unreachable=0    failed=0   

```
```
# ls junos_install_conf/render/
ex4200-12.conf  ex4200-7.conf  ex4200-8.conf

```
```
# more junos_install_conf/render/ex4200-7.conf 
interfaces {
    ge-0/0/1 {
        unit 0 {
            description "ex4200-8";
            family inet {
                address 192.168.10.5/31;
            }
        }
    }
    ge-0/0/0 {
        unit 0 {
            description "ex4200-12";
            family inet {
                address 192.168.10.1/31;
            }
        }
    }
}
protocols {
    replace:
    bgp {
        log-updown
        group underlay {
            import bgp-in;
            export bgp-out;
            type external;
            local-as 209;
            multipath multiple-as;
            neighbor 192.168.10.4 {
                peer-as 210;
            }
            neighbor 192.168.10.0 {
                peer-as 204;
            }
        }
    }
    replace:
    lldp {
        interface "ge-0/0/1";
        interface "ge-0/0/0";
    }
}
routing-options {
    router-id 192.179.0.107;
    forwarding-table {
        export bgp-ecmp;
    }
}

replace:
policy-options {
    policy-statement bgp-ecmp {
        then {
            load-balance per-packet;
        }
    }
    policy-statement bgp-in {
        then accept;
    }
    policy-statement bgp-out {
        then accept;
    }
}
```

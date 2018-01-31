core module.  
https://docs.ansible.com/ansible/2.4/xml_module.html  
requires lxml >= 2.3.0 on host that execute this module.  

```
# ansible-playbook xml/pb_xpath.yml 

PLAY [pass rpc to junos devices, save the output and parse it with xpath] ************************************************************************************************

TASK [get interface information] *****************************************************************************************************************************************
changed: [ex4200-7]

TASK [get neighbor details] **********************************************************************************************************************************************
ok: [ex4200-7]

TASK [debug] *************************************************************************************************************************************************************
ok: [ex4200-7] => {
    "neighbors": {
        "actions": {
            "namespaces": {}, 
            "state": "present", 
            "xpath": "//lldp-neighbor-information[starts-with(lldp-local-interface, 'ge-0/0/')]/lldp-remote-system-name"
        }, 
        "changed": false, 
        "count": 2, 
        "failed": false, 
        "matches": [
            {
                "lldp-remote-system-name": "ex4200-8"
            }, 
            {
                "lldp-remote-system-name": "ex4200-12"
            }
        ], 
        "msg": 2
    }
}

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-7                   : ok=3    changed=1    unreachable=0    failed=0   

```
```
# more xml/ex4200-7.xml 
<lldp-neighbors-information style="brief">
<lldp-neighbor-information>
<lldp-local-interface>ge-0/0/1.0</lldp-local-interface>
<lldp-local-parent-interface-name>-</lldp-local-parent-interface-name>
<lldp-remote-chassis-id-subtype>Mac address</lldp-remote-chassis-id-subtype>
<lldp-remote-chassis-id>00:23:9c:07:da:c0</lldp-remote-chassis-id>
<lldp-remote-port-description>ex4200-7</lldp-remote-port-description>
<lldp-remote-system-name>ex4200-8</lldp-remote-system-name>
</lldp-neighbor-information>
<lldp-neighbor-information>
<lldp-local-interface>ge-0/0/0.0</lldp-local-interface>
<lldp-local-parent-interface-name>-</lldp-local-parent-interface-name>
<lldp-remote-chassis-id-subtype>Mac address</lldp-remote-chassis-id-subtype>
<lldp-remote-chassis-id>2c:6b:f5:94:b1:00</lldp-remote-chassis-id>
<lldp-remote-port-description>ex4200-7</lldp-remote-port-description>
<lldp-remote-system-name>ex4200-12</lldp-remote-system-name>
</lldp-neighbor-information>
</lldp-neighbors-information>
```




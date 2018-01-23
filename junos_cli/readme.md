Module: junos_cli  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.4.3/   
Execute CLI on device and save the output on Ansible    
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download it to the Ansible server, execute the command: ```ansible-galaxy install Juniper.junos,1.4.3```  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf on junos.  

Playbooks:
- **pb_txt.yml**: pass cli to junos devices. Save output in text format  
- **pb_xml.yml**: pass cli to junos devices. Save output in XML format  
- **pb_collect_cli_output.yml**: pass a list a cli (from the file **cli.yml**) to junos devices and save the output in the directory **cli** 

Usage:   
```
# ls junos_cli/
cli.yml cli.log  pb_txt.yml  pb_xml.yml  readme.md
```
```
# ansible-playbook junos_cli/pb_txt.yml 

PLAY [pass cli and save output] ******************************************************************************************************************************************

TASK [junos cli] *********************************************************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-8]
ok: [ex4200-7]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=1    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=0    unreachable=0    failed=0   
```
```
# ls junos_cli/
cli.yml cli.log  ex4200-12.txt  ex4200-7.txt  ex4200-8.txt  pb_txt.yml  pb_xml.yml  readme.md
```
```
# more junos_cli/ex4200-7.txt 

Hardware inventory:
Item             Version  Part number  Serial number     Description
Chassis                                BP0208111225      EX4200-48T
Routing Engine 0 REV 07   750-021254   BP0208111225      EX4200-48T, 8 POE
FPC 0            REV 07   750-021254   BP0208111225      EX4200-48T, 8 POE
  CPU                     BUILTIN      BUILTIN           FPC CPU
  PIC 0                   BUILTIN      BUILTIN           48x 10/100/1000 Base-T
Power Supply 0   REV 02   740-020957   AT0508118512      PS 320W AC
Fan Tray                                                 Fan Tray
```
```
# ansible-playbook junos_cli/pb_xml.yml 

PLAY [pass cli and save output, in xml] **********************************************************************************************************************************

TASK [junos cli] *********************************************************************************************************************************************************
ok: [ex4200-12]
ok: [ex4200-7]
ok: [ex4200-8]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=1    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=0    unreachable=0    failed=0   
```
```
# ls junos_cli/
cli.yml cli.log  ex4200-12.txt  ex4200-12.xml  ex4200-7.txt  ex4200-7.xml  ex4200-8.txt  ex4200-8.xml  pb_txt.yml  pb_xml.yml  readme.md
```

```
# more junos_cli/ex4200-7.xml 
<chassis-inventory>
<chassis style="inventory">
<name>Chassis</name>
<serial-number>BP0208111225</serial-number>
<description>EX4200-48T</description>
<chassis-module>
<name>Routing Engine 0</name>
<version>REV 07</version>
<part-number>750-021254</part-number>
<serial-number>BP0208111225</serial-number>
<description>EX4200-48T, 8 POE</description>
<clei-code>COMU200CRA</clei-code>
<model-number>EX4200-48T</model-number>
</chassis-module>
<chassis-module>
<name>FPC 0</name>
<version>REV 07</version>
<part-number>750-021254</part-number>
<serial-number>BP0208111225</serial-number>
<description>EX4200-48T, 8 POE</description>
<clei-code>COMU200CRA</clei-code>
<model-number>EX4200-48T</model-number>
<chassis-sub-module>
<name>CPU</name>
<part-number>BUILTIN</part-number>
<serial-number>BUILTIN</serial-number>
<description>FPC CPU</description>
</chassis-sub-module>
<chassis-sub-module>
<name>PIC 0</name>
<part-number>BUILTIN</part-number>
<serial-number>BUILTIN</serial-number>
<description>48x 10/100/1000 Base-T</description>
<clei-code>COMU200CRA</clei-code>
<model-number>EX4200-48T</model-number>
</chassis-sub-module>
</chassis-module>
<chassis-module>
<name>Power Supply 0</name>
<version>REV 02</version>
<part-number>740-020957</part-number>
<serial-number>AT0508118512</serial-number>
<description>PS 320W AC</description>
<clei-code>COUPACCEAA</clei-code>
<model-number>EX-PWR-320-AC</model-number>
</chassis-module>
<chassis-module>
<name>Fan Tray</name>
<description>Fan Tray</description>
</chassis-module>
</chassis>
</chassis-inventory>
```
```
# more junos_cli/cli.yml 
---
cli:
    - "show chassis hardware"
    - "show version"
    - "show lldp neighbors"
    - "show bgp neighbor"
    - "show interfaces terse"
    - "show vlans"
    - "show configuration"
    - "show configuration | display set"

```
```
# ansible-playbook junos_cli/pb_collect_cli_output.yml 

PLAY [create cli directories] ********************************************************************************************************************************************

TASK [create cli directory] **********************************************************************************************************************************************
changed: [localhost]

PLAY [pass cli to junos devices] *****************************************************************************************************************************************

TASK [create cli subdirectories] *****************************************************************************************************************************************
changed: [ex4200-7]
changed: [ex4200-8]
changed: [ex4200-12]

TASK [pass the junos cli from the files cli.yml and save the output in the dir cli] **************************************************************************************
ok: [ex4200-12] => (item=show chassis hardware)
ok: [ex4200-8] => (item=show chassis hardware)
ok: [ex4200-7] => (item=show chassis hardware)
ok: [ex4200-12] => (item=show version)
ok: [ex4200-7] => (item=show version)
ok: [ex4200-8] => (item=show version)
ok: [ex4200-12] => (item=show lldp neighbors)
ok: [ex4200-7] => (item=show lldp neighbors)
ok: [ex4200-8] => (item=show lldp neighbors)
ok: [ex4200-12] => (item=show bgp neighbor)
ok: [ex4200-12] => (item=show interfaces terse)
ok: [ex4200-7] => (item=show bgp neighbor)
ok: [ex4200-8] => (item=show bgp neighbor)
ok: [ex4200-12] => (item=show vlans)
ok: [ex4200-8] => (item=show interfaces terse)
ok: [ex4200-7] => (item=show interfaces terse)
ok: [ex4200-12] => (item=show configuration)
ok: [ex4200-7] => (item=show vlans)
ok: [ex4200-12] => (item=show configuration | display set)
ok: [ex4200-8] => (item=show vlans)
ok: [ex4200-7] => (item=show configuration)
ok: [ex4200-8] => (item=show configuration)
ok: [ex4200-7] => (item=show configuration | display set)
ok: [ex4200-8] => (item=show configuration | display set)

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=2    changed=1    unreachable=0    failed=0   
ex4200-7                   : ok=2    changed=1    unreachable=0    failed=0   
ex4200-8                   : ok=2    changed=1    unreachable=0    failed=0   
localhost                  : ok=1    changed=1    unreachable=0    failed=0   
```
```
# ls junos_cli/cli
ex4200-12  ex4200-7  ex4200-8
```
```
# ls junos_cli/cli/ex4200-12/
show bgp neighbor.txt      show configuration | display set.txt  show interfaces terse.txt  show version.txt
show chassis hardware.txt  show configuration.txt                show lldp neighbors.txt    show vlans.txt
```
```
root@ubuntu:~/ansible-training-for-junos-automation# more junos_cli/cli/ex4200-12/"show chassis hardware.txt"

Hardware inventory:
Item             Version  Part number  Serial number     Description
Chassis                                BM0210118007      EX4200-24T
Routing Engine 0 REV 22   750-021256   BM0210118007      EX4200-24T, 8 POE
FPC 0            REV 22   750-021256   BM0210118007      EX4200-24T, 8 POE
  CPU                     BUILTIN      BUILTIN           FPC CPU
  PIC 0                   BUILTIN      BUILTIN           24x 10/100/1000 Base-T
Power Supply 0   REV 04   740-020957   AT0510055247      PS 320W AC
Fan Tray                                                 Fan Tray

```

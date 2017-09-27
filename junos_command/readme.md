Module: junos_command  
Executes commands (cli or rpc) on Junos devices and return the results to the Ansible playbook.     
In addition, it can specify a set of conditionals (with the optional argument waitfor) to be evaluated against the returned output, only returning control to the playbook once the entire set of conditionals has been met (or after a configured timeout). If the conditional is not true by the configured timeout (retries and interval arguments), the task fails for the host. So you can check if you bgp neighbors are established as example.  
Documentation: http://docs.ansible.com/ansible/junos_command_module.html  
source code: https://github.com/ansible/ansible-modules-core/tree/devel/network/junos  
Installation: this is a core module. It ships with ansible itself      
Requirements on Ansible: Ansible 2.1 and junos-eznc   
Requirements on  Junos devices: netconf  

Playbooks:  
- **pb.check.bgp.yml**: check if your bgp neighbors are established.  You first need to configure BGP on your devices otherwise the task will fail. You can use one of these BGP playbooks to configure BGP on your devices  https://github.com/ksator/ansible-training-for-junos/tree/master/junos_template
- **pb.check.bgp_2.yml**: check if your bgp neighbors are established.  You first need to configure BGP on your devices otherwise the task will fail. You can use one of these BGP playbooks to configure BGP on your devices  https://github.com/ksator/ansible-training-for-junos/tree/master/junos_template
- **pb.check.routes.yml**: check details in the device routing table. You first need to configure BGP on your devices otherwise the task will fail. You can use one of these BGP  playbooks to configure BGP on your devices  https://github.com/ksator/ansible-training-for-junos/tree/master/junos_template   
- **pb.check.routes.2.yml**: check details in the device routing table.  You first need to configure BGP on your devices otherwise the task will fail. You can use one of these BGP  playbooks to configure BGP on your devices  https://github.com/ksator/ansible-training-for-junos/tree/master/junos_template
- **pb.check.routes.3.yml**: check details in the device routing table. You first need to configure BGP on your devices otherwise the task will fail. You can use one of these BGP  playbooks to configure BGP on your devices  https://github.com/ksator/ansible-training-for-junos/tree/master/junos_template  
- **pb.check.physical.topology.yml**: check various things on Junos devices like interfaces operational states (are they up?), lldp neighbors (is there any cabling error?), netconf API (is it configured?), ...  
- **pb.check_lldp.yml**: check if the lldp neighbors are the ones we expect (so check if there is no cabling error).  you first need to configure LLDP on your devices.  
- **pb.check.vlans.yml**: check from devices operationnal state if desirated vlans are presents. you first need to configure these VLANs  on your devices.  you can use this playbook to congifure the VLANs on your device  https://github.com/ksator/ansible-training-for-junos/blob/master/junos_config/pb.vlans.yml  
- **pb.yml**: pass various commands on Junos devices. Parse the commands output. Print on Ansible some details gathered from the device. Save the output on the Ansible server.   
- **pb.rpc.yml**: pass rpc to Junos devices. And print on Ansible the result in JSON and XML format.  
- **pb.rpc3.yml**: pass rpc to audit BGP state.  

Usage:  
```
ansible-playbook junos_template/pb.bgp.yml
ansible-playbook junos_command/pb.check.bgp.yml
ansible-playbook junos_command/pb.check.bgp_2.yml
ansible-playbook junos_command/pb.check.routes.yml
ansible-playbook junos_command/pb.check.routes.2.yml
ansible-playbook junos_command/pb.check.routes.3.yml
ansible-playbook junos_command/pb.check_lldp.yml  
ansible-playbook junos_command/pb.check.physical.topology.yml
ansible-playbook junos_rollback/pb.yml

ansible-playbook junos_config/pb.vlans.yml
ansible-playbook junos_command/pb.check.vlans.yml
ansible-playbook junos_config/pb.rollback.yml

ansible-playbook junos_command/pb.yml
ansible-playbook junos_command/pb.rpc.yml

```

This ansible module provide a diff output from devices based on Ansible versions.  
So the parsing (using the wait_for optionnal argument from this module) depends on Ansible versions.    
Above playbooks have been tested with Ansible 2.1/2.2
For other Ansible versions, see below examples  

Ansible 2.3.2 parsing for json output from ex4200-24t running Junos 15.1R2.9:  

```
ksator@ubuntu:~/ansible-training-for-junos-automation$ more junos_command/pb.check.bgp.yml
---
 - name: check bgp states
   hosts: ex4200-12
   connection: local
   gather_facts: no
   # ansible 2.3.2 parsing for json output from ex4200-24t running Junos 15.1R2.9
   tasks:

   - name: check if bgp neighbors are established
     junos_command:
      provider: "{{  credentials }}"
      display: json
      commands:
       - show bgp neighbor "{{ item.peer_ip }}"
      waitfor:
       - "result[0].bgp-information[0].bgp-peer[0].peer-state[0].data eq Established"
     register: bgpdetails
     with_items:
      - "{{ neighbors }}"

   - name: check if bgp neighbors are established using another sysntax
     junos_command:
      provider: "{{  credentials }}"
      display: json
      commands:
       - show bgp neighbor "{{ item.peer_ip }}"
      waitfor:
        - "result[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data'] eq Established"
     register: bgp
     with_items:
      - "{{ neighbors }}"

   - name: print bgp state for item number 0
     debug: 
       msg="bgp session state for item 0 is {{ bgp.results[0].stdout[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data'] }}"

   - name: print bgp state for item number 1
     debug:
       msg="bgp session state for item 1 is {{bgp.results[1].stdout[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data']}}"

   - name: "print bgp states for all items"
     debug:
        msg="bgp state is {{ item.stdout[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data'] }}"
     with_items: "{{ bgp['results'] }}"
     no_log: True

   - name: assert bgp state is established for item number 0
     assert:
       that:
       - "'Established' in bgp.results[0].stdout[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data']"
       msg: "bgp state on device {{ inventory_hostname }} is not established"

   - name: assert bgp state is established for item number 1
     assert:
       that:
       - "bgp.results[1].stdout[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data'] == 'Established'"
       msg: "bgp state on device {{ inventory_hostname }} is not established"

   - name: assert bgp state is established for all items
     assert:
       that:
       - "item.stdout[0]['bgp-information'][0]['bgp-peer'][0]['peer-state'][0]['data'] == 'Established'"
       msg: "bgp state on device {{ inventory_hostname }} is not established"
     with_items: "{{ bgp['results'] }}"
     no_log: True

```
```
ksator@ubuntu:~/ansible-training-for-junos-automation$ ansible-playbook junos_command/pb.check.bgp.yml

PLAY [check bgp states] ***********************************************************************************************************************************************************

TASK [check if bgp neighbors are established] *************************************************************************************************************************************
ok: [ex4200-12] => (item={u'peer_loopback': u'192.179.0.107', u'local_ip': u'192.168.10.0', u'peer_ip': u'192.168.10.1', u'interface': u'ge-0/0/0', u'asn': 209, u'name': u'ex4200-7'})
ok: [ex4200-12] => (item={u'peer_loopback': u'192.179.0.108', u'local_ip': u'192.168.10.3', u'peer_ip': u'192.168.10.2', u'interface': u'ge-0/0/1', u'asn': 210, u'name': u'ex4200-8'})

TASK [check if bgp neighbors are established using another sysntax] ***************************************************************************************************************
ok: [ex4200-12] => (item={u'peer_loopback': u'192.179.0.107', u'local_ip': u'192.168.10.0', u'peer_ip': u'192.168.10.1', u'interface': u'ge-0/0/0', u'asn': 209, u'name': u'ex4200-7'})
ok: [ex4200-12] => (item={u'peer_loopback': u'192.179.0.108', u'local_ip': u'192.168.10.3', u'peer_ip': u'192.168.10.2', u'interface': u'ge-0/0/1', u'asn': 210, u'name': u'ex4200-8'})

TASK [print bgp state for item number 0] ******************************************************************************************************************************************
ok: [ex4200-12] => {
    "msg": "bgp session state for item 0 is Established"
}

TASK [print bgp state for item number 1] ******************************************************************************************************************************************
ok: [ex4200-12] => {
    "msg": "bgp session state for item 1 is Established"
}

TASK [print bgp states for all items] *********************************************************************************************************************************************
ok: [ex4200-12] => (item=(censored due to no_log)) => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result"}
ok: [ex4200-12] => (item=(censored due to no_log)) => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result"}

TASK [assert bgp state is established for item number 0] **************************************************************************************************************************
ok: [ex4200-12] => {
    "changed": false, 
    "msg": "All assertions passed"
}

TASK [assert bgp state is established for item number 1] **************************************************************************************************************************
ok: [ex4200-12] => {
    "changed": false, 
    "msg": "All assertions passed"
}

TASK [assert bgp state is established for all items] ******************************************************************************************************************************
ok: [ex4200-12] => (item=(censored due to no_log)) => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result"}
ok: [ex4200-12] => (item=(censored due to no_log)) => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result"}

PLAY RECAP ************************************************************************************************************************************************************************
ex4200-12                  : ok=8    changed=0    unreachable=0    failed=0   

ksator@ubuntu:~/ansible-training-for-junos-automation$ 
```

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
ansible-playbook rollback/pb.yml

ansible-playbook junos_config/pb.vlans.yml
ansible-playbook junos_command/pb.check.vlans.yml
ansible-playbook junos_config/pb.rollback.yml

ansible-playbook junos_command/pb.yml
ansible-playbook junos_command/pb.rpc.yml

```

Module: junos_get_config  
Documentation: http://junos-ansible-modules.readthedocs.io/en/1.4.3/  
Installation: Hosted on the Ansible Galaxy website (https://galaxy.ansible.com/Juniper/junos/). To download and install it to the Ansible server, execute the command ```ansible-galaxy install Juniper.junos,1.4.3```  
Requirement on Ansible: junos-eznc  
Requirement on Junos devices: enable netconf  

Playbooks: 
- **pb_junos_get_config.yml**: It retrieves junos configuration from junos devices and save it to a file in the **configs** directory on the Ansible server. This will fail if the configs directory doesnt exist on the Ansible server.
- **pb_make_clean.yml**: It makes sure the **configs** directory exists, and removes the old files from the **configs** directory for each host.  
- **pb.yml**: it includes **pb_make_clean.yml** and **pb_junos_get_config.yml** playbooks.  
- **pb_2.yml**: it does the same thing as **pb.yml**, with a different filter (so it retrieves another part of the junos configuration file)  
 
Usage:
```
# ls junos_get_config/
junos_get_config.log  pb_2.yml  pb_junos_get_config.yml  pb_make_clean.yml  pb.yml  readme.md  vars.yml
```
```
# ansible-playbook junos_get_config/pb_make_clean.yml 

PLAY [create a directory] ************************************************************************************************************************************************

TASK [create a directory] ************************************************************************************************************************************************
changed: [localhost]

PLAY [remove old files from the directory for each host] *****************************************************************************************************************

TASK [remove old files from the configs directory for each host] *********************************************************************************************************
ok: [ex4200-7]
ok: [ex4200-8]
ok: [ex4200-12]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=1    changed=0    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=0    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=0    unreachable=0    failed=0   
localhost                  : ok=1    changed=1    unreachable=0    failed=0   
```
```
# ls junos_get_config/
configs  junos_get_config.log  pb_2.yml  pb_junos_get_config.yml  pb_make_clean.yml  pb.yml  readme.md  vars.yml
```
```
# ansible-playbook junos_get_config/pb_junos_get_config.yml 

PLAY [Retrieve configuration from Junos devices] *************************************************************************************************************************

TASK [Retrieve configuration from Junos devices] *************************************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-8]
changed: [ex4200-7]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=1    changed=1    unreachable=0    failed=0   
ex4200-7                   : ok=1    changed=1    unreachable=0    failed=0   
ex4200-8                   : ok=1    changed=1    unreachable=0    failed=0   
```
```
# ls junos_get_config/configs/
ex4200-12.conf  ex4200-7.conf  ex4200-8.conf
```
```
# more junos_get_config/configs/ex4200-12.conf 

## Last changed: 2017-12-01 16:06:40 CET
system {
    host-name ex4200-12;
    domain-name poc-nl.jnpr.net;
    time-zone Europe/Amsterdam;
    authentication-order radius;
    root-authentication {
        encrypted-password "$1$/NHg28eO$pqaVlLlPQ2thlQQ0ZB.Vx/";
    }
    name-server {
        172.30.179.2;
        172.30.179.3;
    }
    radius-server {
        172.30.176.9 {
            secret "$9$DMHPTz36CtOqmBEclLXik.mfT6/t1Eyn/";
            retry 3;
        }
        172.30.176.4 {
            secret "$9$CgY9p1EcylvWx0B7VwgUDtuOBIEleWNVYre";
            retry 3;
        }
    }
    login {
        user remote {
            uid 2000;
            class super-user;
        }
    }
    services {
        ftp;
        ssh {
            client-alive-interval 120;
        }
        telnet;
        xnm-clear-text;
        netconf {
            ssh;
        }
        web-management {
            http;
        }
    }
    syslog {
        user * {
            any emergency;
        }
        host 172.30.189.13 {
            any notice;
            authorization info;
            interactive-commands info;
        }
        host 172.30.189.14 {
            any notice;
            authorization info;
            interactive-commands info;
        }
        file messages {
            any notice;
            authorization info;
        }
    }
    compress-configuration-files;
    commit synchronize;
    ntp {
        boot-server 172.30.179.3;
        server 172.30.179.3;
        server 172.30.179.2;
    }
}
```
```
# ansible-playbook junos_get_config/pb.yml 

PLAY [create a directory] ************************************************************************************************************************************************

TASK [create a directory] ************************************************************************************************************************************************
ok: [localhost]

PLAY [remove old files from the directory for each host] *****************************************************************************************************************

TASK [remove old files from the configs directory for each host] *********************************************************************************************************
changed: [ex4200-7]
changed: [ex4200-8]
changed: [ex4200-12]

PLAY [Retrieve configuration from Junos devices] *************************************************************************************************************************

TASK [Retrieve configuration from Junos devices] *************************************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-8]
changed: [ex4200-7]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=2    changed=2    unreachable=0    failed=0   
ex4200-7                   : ok=2    changed=2    unreachable=0    failed=0   
ex4200-8                   : ok=2    changed=2    unreachable=0    failed=0   
localhost                  : ok=1    changed=0    unreachable=0    failed=0   

```
```
# ansible-playbook junos_get_config/pb_2.yml

PLAY [create a directory] ************************************************************************************************************************************************

TASK [create a directory] ************************************************************************************************************************************************
ok: [localhost]

PLAY [Retrieve configuration from junos devices] *************************************************************************************************************************

TASK [remove old files from the configs directory for each host] *********************************************************************************************************
changed: [ex4200-7]
changed: [ex4200-8]
changed: [ex4200-12]

TASK [include vars] ******************************************************************************************************************************************************
ok: [ex4200-7]
ok: [ex4200-8]
ok: [ex4200-12]

TASK [Retrieve configuration from junos devices] *************************************************************************************************************************
changed: [ex4200-12]
changed: [ex4200-7]
changed: [ex4200-8]

PLAY RECAP ***************************************************************************************************************************************************************
ex4200-12                  : ok=3    changed=2    unreachable=0    failed=0   
ex4200-7                   : ok=3    changed=2    unreachable=0    failed=0   
ex4200-8                   : ok=3    changed=2    unreachable=0    failed=0   
localhost                  : ok=1    changed=0    unreachable=0    failed=0   

```

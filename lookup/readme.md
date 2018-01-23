lookup allows Ansible to access data from outside sources (files ...)  
Doc: http://docs.ansible.com/ansible/playbooks_lookups.html  

playbook: 
- **pb.yml**: this pb uses various lookups to get the current time from the Ansible server, and print the time using the debug module.  

usage: 

```
# ansible-playbook lookup/pb.yml 

PLAY [Get date] **********************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************
ok: [localhost]

TASK [date1] *************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Tue Jan 23 03:42:01 PST 2018"
}

TASK [date2] *************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "0123-034201"
}

PLAY RECAP ***************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0   

```



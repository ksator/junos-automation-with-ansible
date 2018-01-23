apt is a core module
http://docs.ansible.com/ansible/apt_module.html  
it manages packages on ubuntu: you can use it to install/remove packages on ubuntu endpoints.     
it is idempotent.  

```
# ansible-playbook apt/pb.yml -u ksator --ask-sudo-pass --check --diff
SUDO password: 

PLAY [install latest apache2 on localhost] *******************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************
ok: [localhost]

TASK [install latest apache2] ********************************************************************************************************************************************
The following extra packages will be installed:
  apache2-bin apache2-data libapr1 libaprutil1 libaprutil1-dbd-sqlite3
  libaprutil1-ldap
Suggested packages:
  apache2-doc apache2-suexec-pristine apache2-suexec-custom apache2-utils
The following NEW packages will be installed:
  apache2 apache2-bin apache2-data libapr1 libaprutil1 libaprutil1-dbd-sqlite3
  libaprutil1-ldap
0 upgraded, 7 newly installed, 0 to remove and 162 not upgraded.
changed: [localhost]

PLAY RECAP ***************************************************************************************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0   

```

```
# apt list --installed | grep apache

```
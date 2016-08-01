apt is a core module
http://docs.ansible.com/ansible/apt_module.html  
it manages packages on ubuntu: you can use it to install/remove packages on ubuntu endpoints.     
it is idempotent.  

```
$ ansible-playbook --help
$ ansible-playbook apt/pb.yml -u ksator --ask-sudo-pass --check --diff
SUDO password: 
[DEPRECATION WARNING]: Instead of sudo/sudo_user, use become/become_user and make sure become_method is 'sudo' (default).
This feature will be removed in a future release. 
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.

PLAY [[install latest apache2 on localhost] ************************************

TASK [setup] *******************************************************************
ok: [localhost]

TASK [install apache2] *********************************************************
changed: [localhost]
The following packages were automatically installed and are no longer required:
  bsdtar libgsoap4 libruby1.9.1 ruby ruby-childprocess ruby-erubis ruby-ffi
  ruby-i18n ruby-log4r ruby-net-scp ruby-net-ssh ruby1.9.1 virtualbox-dkms
Use 'apt-get autoremove' to remove them.
The following extra packages will be installed:
  apache2-bin apache2-data libapr1 libaprutil1 libaprutil1-dbd-sqlite3
  libaprutil1-ldap
Suggested packages:
  apache2-doc apache2-suexec-pristine apache2-suexec-custom apache2-utils
The following NEW packages will be installed:
  apache2 apache2-bin apache2-data libapr1 libaprutil1 libaprutil1-dbd-sqlite3
  libaprutil1-ldap
0 upgraded, 7 newly installed, 0 to remove and 371 not upgraded.

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0   

$ apt list --installed | grep apache
WARNING: apt does not have a stable CLI interface yet. Use with caution in scripts.


```


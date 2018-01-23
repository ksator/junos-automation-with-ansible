Module: shell
Executes commands
Documentation : http://docs.ansible.com/ansible/shell_module.html  
Installation: this is a core module. It ships with ansible itself  

Playbooks:  
- **pb_git.yml**: it uses the ansible module **template** to create the junos configuration for junos devices based on the template **initial_configuration.j2**. The junos configuration files created are stored in the local directory. Nothing is loaded on Junos devices. Then the rendered configuration files are pushed to the remote git repository.


Usage:   
```
# ls shell/
initial_configuration.j2  pb_git.retry  pb_git.yml  readme.md
```
```
# ansible-playbook shell/pb_git.yml --extra-var comment=git_push_from_ansible

PLAY [render template to create junos configuration] *********************************************************************************************************************

TASK [Render initial configuration for junos devices] ********************************************************************************************************************
changed: [ex4300-18]
changed: [ex4300-17]
changed: [ex4300-9]

PLAY [push to the remote git repository in the master branch] ************************************************************************************************************

TASK [command] ***********************************************************************************************************************************************************
changed: [localhost]

TASK [command] ***********************************************************************************************************************************************************
changed: [localhost]

TASK [command] ***********************************************************************************************************************************************************
Username for 'https://github.com': ksator
Password for 'https://ksator@github.com': 
changed: [localhost]

PLAY RECAP ***************************************************************************************************************************************************************
ex4300-17                  : ok=1    changed=1    unreachable=0    failed=0   
ex4300-18                  : ok=1    changed=1    unreachable=0    failed=0   
ex4300-9                   : ok=1    changed=1    unreachable=0    failed=0   
localhost                  : ok=3    changed=3    unreachable=0    failed=0   

```
```
# ls shell/
ex4300-17.initial_configuration.conf  ex4300-9.initial_configuration.conf  pb_git.retry  readme.md
ex4300-18.initial_configuration.conf  initial_configuration.j2             pb_git.yml
```
```
# git log -n 1 --oneline
0a1c095 git_push_from_ansible
```
```
# git status 
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working directory clean
```

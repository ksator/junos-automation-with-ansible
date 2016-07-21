This project has many ready to use Ansible playbooks to interact with Junos devices.     

The default ansible 'hosts' file lives in /etc/ansible/hosts  
The inventory file I am using in this repository is hosts.   
It is at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/hosts)  

There is an ansible.cfg file at the root of the repository (https://github.com/ksator/ansible-training-for-junos/blob/master/ansible.cfg) that refers to this inventory file.   
So, no need to add -i hosts to your ansible-playbook commands.  

Download the content and use ansible-playbook commands to execute playbooks:  
git clone https://github.com/ksator/ansible-training-for-junos.git  
cd ansible-training-for-junos/    
ansible-playbook xxx/pb.yml  




# Ansible Galaxy

### **Chapter Note!**
### Error with Python version and ansible-galaxy install
Make sure pip package manager is installed
`curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py`
`python get-pip.py`
clean up
`rm get-pip.py`
## Use pip to install missing packages
`pip install urllib3 pyOpenSSL ndg-httpsclient pyasn1`

## Selecting Roles for HAProxy

Proxy Used
[haproxy](https://galaxy.ansible.com/geerlingguy/haproxy)

## Applying HAProxy role with custom properties

## Troubleshooting HAProxy issues
http://142.93.75.12/app/
## Nano Project: Seup MySQL DB using a galaxy role

## Setting up MySQL

## Connecting app with the database

## Checking in the galaxy roles
[defaults]  
remote_user = devops  
inventory   = environments/prod  
retry_files_save_path = /tmp  
host_key_checking = False  
log_path=~/ansible.log  
hash_behaviour = merge  
**roles_path = roles:galaxy-roles**  

## Tagging tasks, roles, plays, and playbook
You can tag roles, task, plays, site.yml, which can be displayed before applying playbooks and roles  
`ansible-playbook --help | grep -i tag`  
`ansible-playbook  app.yml  --list-tags`  
`ansible-playbook  app.yml  --list-task`  
Example of applying tags
NOTE: tags are inherited from the `roles->playbook->site.yml`
```
---
  - hosts: app
    become: true
    vars:
      fav:
        fruit: mango
    roles:
      - {role: apache, tags: www }
      - {role: php, tags: ['www', 'php'] }
      - {role: frontend, when: ansible_os_family == 'RedHat', tags: devopsdemo}
    tags:
      - frontend
```
You can call the playbook based on the tag name
`ansible-playbook site.yml --tags=app.config` 

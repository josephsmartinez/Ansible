# Auto Discovery and Managing Multiple Environments

## Enable Facts Caching

Notice that `fact_caching` & `fact_caching_connection` have been added  
```
[defaults]

remote_user = devops
inventory   = environments/prod
retry_files_save_path = /tmp
host_key_checking = False
log_path=~/ansible.log
hash_behaviour = merge
roles_path = roles:galaxy-roles
fact_caching = yaml
fact_caching_connection = /tmp/facts
```
**watch command**  
`watch -n l ls -l /tmp/facts`  
`ansible-dic -t cache -l`  

## Using Magic Variables for Service Discovery

**REDO SECTION**

## Creating Staging Environment

ansible-playbook -i environment/staging site.yml --list-hosts  

**REDO SECTION**  


## Rolling Back Changes with Contra Playbooks

Example of a rollback Playbook `chap10/cleanup.yml` intended to be the opposite of configuration files/install playbooks.  
```
---
  - name: cleanup database server
    hosts: db
    become: true
    tasks:
      - name: stop mysql service
        service:
          name: mysqld
          state: stopped

      - name: uninstall mysql related packages
        package:
          name: "{{ item }}"
          state: absent
        with_item:
          - mysql-server
          - mysql
```

Resources:

Magic Variables   
https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html

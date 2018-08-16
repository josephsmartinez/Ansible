## Problem Statement

You have to create a playbook for base systems
configuration. Common configurations for all hosts are,

- **admin** user should be present with uid **5001**
- user **dojo** should not have an account on any host
- install **tree**
- install **ntp**

on all systems which belong to **prod** group in the
inventory



### SOLUTION TRY A SYNTAX TEST AND DRY RUN
```
---
    - name: base systems configuration for linux servers
      hosts: pord
      become: true
      task:
        - name: create admin
          user:                 # Module
            name: admin
            state: present
            uid: 5001

        - name: remove user dojo id present
            user: >
                name=dojo
                state=absent

        - name: install tree
            yum: |
                name=tree
                state=present

        - name: install ntp
            yum:
                name: ntp
                state: installed
```

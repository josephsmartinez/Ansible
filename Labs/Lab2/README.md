# Problem Statement

###You have to create a playbook for base systems
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
    - name: base systems configuration for Linux servers
      hosts: prod # 'prod:!db:!app1' <-- Other option
      become: true
      tasks:

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

# Example Log
```
2018-08-16 02:35:24,086 p=6158 u=root |  PLAY [base systems configuration for linux servers] *********************************
2018-08-16 02:35:24,101 p=6158 u=root |  TASK [Gathering Facts] **************************************************************
2018-08-16 02:35:43,255 p=6158 u=root |  ok: [db]
2018-08-16 02:35:43,277 p=6158 u=root |  ok: [app2]
2018-08-16 02:35:43,289 p=6158 u=root |  ok: [app1]
2018-08-16 02:35:43,313 p=6158 u=root |  ok: [lb]
2018-08-16 02:35:43,319 p=6158 u=root |  TASK [create admin] *****************************************************************
2018-08-16 02:35:45,969 p=6158 u=root |  changed: [app2]
2018-08-16 02:35:45,973 p=6158 u=root |  changed: [db]
2018-08-16 02:35:45,978 p=6158 u=root |  changed: [lb]
2018-08-16 02:35:45,981 p=6158 u=root |  changed: [app1]
2018-08-16 02:35:45,988 p=6158 u=root |  TASK [remove user dojo id present] **************************************************
2018-08-16 02:35:46,997 p=6158 u=root |  ok: [lb]
2018-08-16 02:35:47,059 p=6158 u=root |  ok: [app1]
2018-08-16 02:35:47,115 p=6158 u=root |  ok: [app2]
2018-08-16 02:35:47,128 p=6158 u=root |  ok: [db]
2018-08-16 02:35:47,137 p=6158 u=root |  TASK [install tree] *****************************************************************
2018-08-16 02:35:56,257 p=6158 u=root |  changed: [app2]
2018-08-16 02:35:56,779 p=6158 u=root |  changed: [db]
2018-08-16 02:35:56,811 p=6158 u=root |  changed: [app1]
2018-08-16 02:35:56,825 p=6158 u=root |  changed: [lb]
2018-08-16 02:35:56,833 p=6158 u=root |  TASK [install ntp] ******************************************************************
2018-08-16 02:36:10,055 p=6158 u=root |  changed: [app1]
2018-08-16 02:36:10,074 p=6158 u=root |  changed: [lb]
2018-08-16 02:36:10,089 p=6158 u=root |  changed: [app2]
2018-08-16 02:36:10,094 p=6158 u=root |  changed: [db]
2018-08-16 02:36:10,098 p=6158 u=root |  PLAY RECAP **************************************************************************
2018-08-16 02:36:10,099 p=6158 u=root |  app1                       : ok=5    changed=3    unreachable=0    failed=0   
2018-08-16 02:36:10,099 p=6158 u=root |  app2                       : ok=5    changed=3    unreachable=0    failed=0   
2018-08-16 02:36:10,099 p=6158 u=root |  db                         : ok=5    changed=3    unreachable=0    failed=0   
2018-08-16 02:36:10,099 p=6158 u=root |  lb                         : ok=5    changed=3    unreachable=0    failed=0   
2018-08-16 02:36:28,023 p=6340 u=root |   [WARNING]: Found both group and host with same name: db
```

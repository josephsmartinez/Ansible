
# Automantion with Ansible

### Scenario
Given an infrastructure with load-balancers,  applications, and data-base, how can we start to use Ansible to automate the tasks needed to orchestrate this kind of infrastructure

### Break the problem into tier levels
- App
    - Create Users
    - Install Apps
    - Manage Configs
    - Start Services

### Modules
```  
    Task Definitions -> Define the state
        - user
            uid = 5001
            home = /home/joe
            pass = pa$$W0rD
            state = present

        - packages
            name = php
            version = 7.0
            state = installed

        - template
            source = package.tar
            owner = root
            mode = 0644
            state = present

        - service
            name = ntp
            state = running
```            
### Tasks file
Each task file has a different objective
```  
    main.yml
        -> user
        -> package
```        

**However task files are not enough...**

### Application Tree

ROLE,
- You will make a role for every application with in the infrastructure.
- Roles should be completely independent of each other to extend them to other projects.
```
       Role
       |
       |-------- Java
       |-------- Tomcat
       |-------- MySql
       |-------- MongoDB
       |
       | app1____ Task
                    |----- ta1.yaml
                |   |----- ta2.yaml
                |
                |Files
                |   |---- f1
                |   |---- f2
                |
                |Vars
                    |---- Main.yml
```                               
### Inventory
```    
    Server - DataBase

    Server -> App

    Server -> Caches and Queue

    Server ->
```

### PlayBook (Mapping)

- Play define the play, and the play defines the mapping betwen servers.

- You will have a play for every catrgory

- Some plays can be common for all

**Example Play Book**
```    
     Play 1 ->  hosts: db
                remote_user: devops
                become: true
                roles:
                - { role: mysql, ... }

     Play 2 ->  hosts: www
                remote_user: devops
                become: true
                roles:
                - { role: base, java ... }

     Play 3 ->  hosts: lb
                remote_user: devops
                become: true
                roles:
                - { role: base, ssl ... }
```
### Code Organization Strategies

**Best Practices*** https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html

### Introduction Use Case - DevOps Demo App

Php Web Application

Load Balancer

Application
- php
- app
- apache

DataBase
- mySql

### Example Code Structure
```    
    ansible-repo
    |
    |---------- environments
    |   |--dev
    |   |--prod
    |
    |
    |---------- group-vars
    |   |--prod
    |   |--dev
    |   |--all
    |
    |---------- roles
    |   |--php
    |   |--apache
    |   |--mysql
    |   |--hproxy
    |   |--systems
    |
    |---site.yml
    |---app.yml             PLAYS
    |---db.yml
    |---lb.yml
    |---systems.yml
    |---update.yml
    |---ansible.cfg
```



# Exercise
### Role to install PHP
- Create a **php** role
- Add task to install **php** and **php-mysql** packages
- Send a notification to restart apache after installing the packages

Start by create the scaffolding of the PHP module
```
ansible-galaxy --offline --init-path=roles php
```

### 1) Build install.yml for php with the task
```
---
  - name: install php packages
    yum:
      name: "{{ item }}"
      state: installed
    with_items:
        - php
        - php-mysql
    notify: restart apache service
```
**Make sure to add the handler as apache needs to restarted after php has been installed**

### 2) Add the install.yml to main.yml within task directory
```
---
# tasks file for php
  - import_tasks: install.yml
```
### 3) Update the app.yml at the root of the project
```
---
  - name: app server playbook
    hosts: app
    become: true
    roles:
      - apache
      - php
```

# Problem Statement

### Create a role for installing and configuration **apache** web server on **CentOS** platform which will:

- Install **httpd** package
- Centrally manage **httpd.conf** and copy it to all nodes
- Start httpd service
- Whenever apache **configs** are updated, relevant **service** should be automatically **restarted**

### Within roles -> apache -> task

install.yml
main.yml
service.yml

### install.yml
```
---
  - name: install apache web server
    yum:
      name: httpd
      state: installed
```
### service.yml
```
---
  - name: install apache web server
    yum:
      name: httpd
      state: started
```
### main.yml
```
---
# tasks file for apache
  - import_tasks: install.yml
  - import_tasks: service.yml
  
```

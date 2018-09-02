# Vars and Templates
## Need to separate data from code
Code vs Data

code </>  templates   port = {{ port }}
          tasks       user = {{ user }}
                      conn = {{ conn }}
--------------------------------------
data [-]  vars        apache_port = 80
          facts       apache_user = httpd
                      conn = 1024
## Diving into Jinja2 templates

- Way to generate dynamic configurations
- Ansible uses Jinja2 template engine
- Along with Variable, can be used to create flexible roles

config => template

- Python based template language
- Compiled just in time into python byte code
- Fast
- Commonly used by Python based automation tools such as ansible, fabric, slat.

### Jinja Templating
Your container.yml may contain Jinja variables and expressions indicated using the default delimiters as follows:
- `{% ... %}` for control statements
- `{{ ... }}` for expressions
- `{# ... #}` for comments

Here’s an example container.yml containing Jinja expressions:
```
version: "1"
services:
  web:
    image: '{{ web_image }}'
    ports: '{{ web_ports }}'
    command: ['sleep', '10']
    dev_overrides:
        environment:
        - DEBUG='{{ debug }}'
registries: {}
```


[Jinja2](http://jinja.pocoo.org/docs/dev/)
[Jinia Templating](https://docs.ansible.com/ansible-container/container_yml/template.html)

### JINJA2
- Contains regular text with dynamic fragments, marked with special tags
- Dynamic fragments are either variables or python code, which is executed at the run time, creating the resulting text files.
- Files are created using .j2 extensions and stored in template directory inside roles.

{{ var }}
{% code %}

### JINJA2 TAGS
...

## Understanding ansible vars, Precedence Levels and Best Practices
Variable Types
User Defined Vars | Automatic Facts

### User Defined Vars
- Roles default Vars
- Inventory Vars : hostvars, groupvars
- Playbook vars
- Roles vars
- Extra Vars at the runtime (-e switch)

### Defining Vars
```
port

port1

mysql_port

mysql:
  port: 3306
  user: mysql
  server: true
```
### Accessing Vars
```
{{ port }}
{{ port1 }}
{{ mysql_port }}

{{ mysql[port] }}
--or--
{{ mysql.port }}
```
### Variable File Separation
It’s a great idea to keep your playbooks under source control, but you may wish to make the playbook source public while keeping certain important variables private. Similarly, sometimes you may just want to keep certain information in different files, away from the main playbook.

You can do this by using an external variables file, or files, just like this:
```
---
- hosts: all
  remote_user: root
  vars:
    favcolor: blue
  vars_files:
    - /vars/external_vars.yml

  tasks:

  - name: this is just a placeholder
    command: /bin/echo foo
```
This removes the risk of sharing sensitive data with others when sharing your playbook source with them.

The contents of each variables file is a simple YAML dictionary, like this:
```
---
# in the above example, this would be vars/external_vars.yml
somevar: somevalue
password: magic
```
[Variables and File Separation](https://docs.ansible.com/ansible/2.5/user_guide/playbooks_variables.html#variable-file-separation)
### Variable Precedence
-e switch           ^
role Vars           |
playbook vars       |
host vars           |
group vars          |
role defaults       |

## Advanced vars concepts
- Example using vars within roles  
- The variables within this role's tasks/main.yml come from defaults and the config file resides within templates  
```
---
# tasks file for frontend

- name: create app directory
  file:
    path: /opt/app
    owner: apache
    group: apache
    mode: 0755
    state: directory

- name: create release path
  file:
    path: /opt/app/release
    owner: apache
    group: apache
    mode: 0755
    state: directory

- name: Download and extract the release
  unarchive:
    src: https://github.com/devopsdemoapps/devops-demo-app/archive/{{ app.version }}.tar.gz
    dest: /opt/app/release
    owner: apache
    group: apache
    creates: /opt/app/release/devops-demo-app-{{ app.version }}
    remote_src: yes

- name: create a symlink
  file:
    src: /opt/app/release/devops-demo-app-{{ app.version }}
    dest: /var/www/html/app
    owner: apache
    group: apache
    state: link

- name: add application configs
  template:
    src: config.ini.j2
    dest: /var/www/html/app/config.ini
    owner: apache
    group: apache
    mode: 0644

```

## Dynamically defining app version with and tasks

## Managing app configs with templates and vars

## Playing with vars precedence
https://schoolofdevops.github.io/ultimate-ansible-bootcamp/templates_and_variables/#beyond-defaults-playing-with-vars-precedence

dump check
```
ansible-config dump
ansible-config dump | grep -i hash
```


## Registered variables and conditional execution

## Discovering facts with setup modules
Setup module and filter
```
ansible all -m setup -a "filter=ansible_os_family"
```
Dump all node facts within /tmp/facts
```
ansible -m setup --tree /tmp/facts
```

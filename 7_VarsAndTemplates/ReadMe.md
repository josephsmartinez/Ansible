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
- Along with Varible, can be used to create flexible roles

config => template

- Python based template language
- Compiled just in time into python byte code
- Fast
- Commonly used by Python based automation tools such as ansible, fabric, slat.

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
### Variable Precedence
-e switch           ^
role Vars           |
playbook vars       |
host vars           |
group vars          |
role defaults       |

## Advanced vars concepts




## Dynamically defining app version with and tasks

## Managing app configs with templates and vars

## Playing with vars precedence

## Registered variables and conditional execution

## Discovering facts with setup modules

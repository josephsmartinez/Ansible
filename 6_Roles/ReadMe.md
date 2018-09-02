# Why roles?
- Address Complexity
- Reusability and Sharing
- Modular Code

### Complexity
- hosts definitions, properties, tasks, all in one place
- Specific to one environment, can not be shared
- Difficult to reuse
- Can quickly get out of control with increasing number of applications

### Modular Approach
```
  roles
  |
  |----Base
  |----Apache
  |----PHP
```
# Anatomy of a Role
"A **role** is a package which contains **tasks** which
**take action** along with supporting entitles such as **handlers, properties, files, tests, and metadata**"

### Anatomy of Roles

- task      -> actions to take, using modules
- defaults  -> default properties/var  
- vars      -> role specific vars
- files     -> static files to be copied to nodes
- templates -> files generated dynamically
- handlers  -> actions to take on events
- tests     -> ansible test
- meta      -> role meta data

### When to create a Role
1 : 1 Mapping

# Code Organization Strategies
 Inventory nodes into layers
 Create roles for all applications
 Common role can be made

When apply applying configuration to all the node, you will call `site.yml`

# Generating Roles Scaffold and Ansible Galaxy
### Two ways to create Roles
- Manual
  - Role can be created by simply creating directories and files in certain order
- Ansible-Galaxy
  - A utility which lets you generate role scaffolding

### Ansible Galaxy
- A **library** of community contributed **roles**
- No need to reinvent the wheel. Reuse and share roles
- Serves as a source to **reference** to learn best practices

### Creating Roles with Galaxy | Scaffolding a Customer Role
`ansible-galaxy init --init-path=roles apache`
`ansible-galaxy --help`

# Create a role for Apache
 Reference Lab5

```
roles/
`-- apache
    |-- README.md
    |-- defaults
    |   `-- main.yml
    |-- files
    |-- handlers
    |   `-- main.yml
    |-- meta
    |   `-- main.yml
    |-- tasks
    |   `-- main.yml
    |-- templates
    |-- tests
    |   |-- inventory
    |   `-- test.yml
    `-- vars
        `-- main.yml
```
### Mapping Action to Modules
**Actions                           Modules**
install httpd              -->    yum or apt
start httpd service        -->    service
copy configs and html docs -->    copy

### Writing Task
- we need to start defining **actions** and its desired state using tasks
- tasks directory in roles comes with **main.yml** as
a default task file
- all action can be defined in main.yml
- however, we will create **individual task** for each action for fine grained control
- and include it from **main.yml**

```
roles
|--apache
   |--tasks
   |--main.yml
   |--install.yml
   |--config.yml
   `--service.yml
```

### Writing a Main Task
File: roles/apache/tasks/main.yml
- when you call a role from playbookm it includes only **main.yml** task file
- if you create additional task files, the only way to have those called is by including in **main.yml**
- lets include install.yml and service.yml in main.yml apache role

# Writing a applying playbook for servers
Creating Playbook for App
- As per our strategy, we are going to create a playbook for each layer
- let us begin by writing app.yml for app servers to apply apache role
- apache role will in turn point to main.yml
- main.yml will then execute all included tasks from  install.yml and start.yml

# Copying config file, notifications, and handlers
```
roles
|--apache
|   |--tasks
|   |--main.yml
|   |--install.yml
|   |--config.yml
|   `--service.yml
|--files
    |--httpd.conf
```
- In addition to installing and starting services, we also need to copy configuration file for apache
- To manage centrally, files are stored in its own dedicated **files** directory inside roles
- in addition, **task** to copy the files from inside roles to appropriate destination need to be created. Let's write **config.yml** to do this
- Which will then be added to **main.yml** just like other two task files we created earlier

NOTE: We must account situations when config files are edited and services must restart. Case: Changing a port on the firewall settings, require that firewall services are restarted. **We need handlers**

### Adding a Handler
- Just like task and files, handles have their own dedicated directory.
- Inside which you may already find main.yml
- You could add handler to restart apache here
- Handler will get triggered only when notified
```
roles
|--apache
|   |--tasks
|   |--main.yml
|   |--install.yml
|   |--config.yml
|   `--service.yml
|--files
|   |--httpd.conf
|   `--index.html
|--handlers
|   `--main.yml
```
### Handler format
Here is an example handlers file. As a review, handlers are only fired when certain tasks report changes, and are run at the end of each play:

Example 1
```
---
# handlers file for apache
  - name: Restart apache service
    service: name=httpd state=restarted
```
Example 2
```
---
# file: roles/common/handlers/main.yml
- name: restart ntpd
  service:
    name: ntpd
    state: restarted
```
[Playbook Best Practices]https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html?highlight=handlers

# Create a role for PHP
 Please review Lab6

# Nested roles and site wide playbook
Please review Lab7

# Nano project: Deploy DevOps Demo App
Please review Lab8

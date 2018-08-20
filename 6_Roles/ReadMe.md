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

### Creating Roles with Galaxy
`ansible-galaxy init --init-path role/apache`
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
- main.yml will then execute all included tasks from install.yml and start.yml





# Copying config file, notifications, and handlers

# Create a role for PHP

# Nested roles and site wide playbook

# Nano project: Deploy DevOps Demo App

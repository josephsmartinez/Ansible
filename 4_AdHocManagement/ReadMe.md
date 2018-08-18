# Ad Hoc Server Management with Ansible

## Configuration Ansible
Default Path:

`/etc/ansible/andible.cfg`

Follow **ini** style configurations
Contains [blocks] of configurations with
**key = value pairs**

## CONFIGS
Configuration file can be created from other paths
too (e.g. 'home','dir','current dir')

`~/ansible.cfg`
`./ansible.cfg`

'ANSIBLE_CONFIG' environment variable can be used to
define configurations path

Parameters can be 'overridden' in 'ansible-playbook' or
with 'command line flags'.

Precedence Level

How ansible knows how to pick which configurations
to pick.
```
CONFIG FILES PRECEDENCE
    ^
    | p1 command line flags
    | p2 ANSIBLE_CONFIG
    | p3 ./ansible.cfg
    | p4 ~/.ansible.cfg
    | p5 /etc/ansible/ansible.cfg
```
### GOOD NEWS

This make sharing, changing, switching base the project

- Overrides defaults
- Revision controlled
- Switching configuration for each project

Best Practice: Its a good idea to create projects
specific configurations inside your workspace

Some useful commands

### Current active configuration and PATH
`ansible --version`

### List view and dumb integration
`ansible-config`

### Current configurations
`ansible-config view`

### Complete configuration added. Orange are custom packages
`ansible-config dump`

### Configuration about the Parameters
`ansible-config list`

------------------------------------------------------

## Defining a static inventory

List of serves ansible is to manage
Think of /etc/hosts file

**ini** format

### EXAMPLE FORMAT
```
[app]
app-01.br.example.org         ---Host Groups
app-02.br.example.org
app-01.bom.example.org
app-02.bom.example.org

[db]
db-01.br.example.org          -- Connection string/host
db-01.bom.example.org

[bir:children]
app                           --Group of groups
db
```
### INVENTORY
Could Contain
- HOST
- GROUP
- CONNECTION PARAMETERS
- HOSTVARS
- GROUPVARS

### EXAMPLE WITH PARAMETERS and VARIABLES
```
    [app]
    app-01.br.example.org
    app-02.br.example.org   ansible_user=vargrant
    app-01.bom.example.org
    app-02.bom.example.org  apache_port=8080 max_connection-400

    [db]
    db-01.br.example.org    ansible_user=centos
    db-01.bom.example.org

    [bir:children]
    app
    db
```
## SSH CONNECTION OPTIONS

### ansible_host
The name of the host connect to different from
the alias you wish to give to it.

### ansible_port
The ssh port number, if not 22

### ansible_user
The default shh user name to use

### ansible_ssh_pass
The ssh password to use (this is insecure, we
strongly recommend using --ask-pass or SHH keys)

## TWO TYPE OF INVENTORIES
**Static** and **Dynamic**

Example
- Create directory to hold env spec. host
- Creating Inventory
```
[local]
localhost ansible_connection=local

[lb]
lb

[app]
app1
app2

[db]
db

[prod:children]
lb
app
```
## SETTING UP SSH
Ansible works over ssh transport, instead of creating its own transport.

1. Generating SSH keys on control node
`ssh-keygen -t rsa`

2. Copy SSH Pub Key to All Inventory Hosts
`ssh-copy-id user@host`

3. Validate Password Login
`ssh user@host`

## SAY HELLO TO NODES
`ansible all -m ping`

------------------------------------------------------
## Host Pattern and Ad Hoc Commands
```
ansible all -m <module> -a <args>
        ---
         ^
         host pattern
```
define hosts or groups of hosts being managed.

### HOST PATTERNS
- wildcards
`all, * , app*, *.example.com`

- hosts/groups
`app1, app1:app2, db, app:lb`

- subscripts
`app[0], app[-1], prod[0:3], prod[2:]``

- exclusion
`!`
`prod:!db`

- intersection
`?`
`prod:&app`

- regex
`~`
`~(app|db)*`

The --limit option can be used along
with ansible and playbook commands to restrict
execution to specific set of host/groups
`--limit`

### COMMAND EXAMPLES
```
ansible all -m ping
ansible '*' -m ping
ansible app* -m ping
ansible all -m ping --limit app
ansible app -m ping --limit app1
ansible prod -m ping --limit lb
ansible prod -m ping --limit lb:app
ansible 'app[0]' -m ping
ansible 'app[-1]' -m ping
ansible 'prod[0:3]' -m ping
ansible 'prod[2:]' -m ping
```
### RUNNING ON ONE HOST AT A TIME
`ansible all -a "free"`

### RUNNING ADHOC COMMANDS
```
ansible '!(app|db).*' -a "hostname"
ansible '*' -a "hostname"
ansible '*' -a "SOME COMMAND TO EXECUTE"
```
### SUDO COMMAND ADHOC
```
ansible '*' -b -a "yum install -y vim"
```
------------------------------------------------------

## Modules and Desired State Configuration

Modules all us to manage 'independent components or
entities' of our infrastructure.

Such as...
- packages
- files
- services
- networking interfaces
- users & groups
- cron jobs
- mount points

## DESIRED STATE
```
user              <-- entity
  name = xyz      <-- properties
  state = present <-- properties
  uid = 5001      <-- properties
  group = admins  <-- properties

MAPPING

  1     :   1    --> Mapping between
System  : Modules
```
## MODULES CATAGORIES
System, Utilities, Packaging, Files, Database,
Networking, Source Control, Command, Clustering,
Web Infrastructure, Notifications, Remote Management,
Windows, Inventory, Messaging, etc...

Total number of available modules
`ansible-doc --list | wc -l`

### MODULES TYPES

**Core**
- Maintained by ansible team
- Always be shipped with ansible

**Extras**
- Maintained by community
- Currently shipped with ansible
- May be shipped separately in the future
------------------------------------------------------
## Invoking Modules Idempotence

## TWO WAY TO USE MODULES

1) Command Line
`ansible app -m yum -s -a "name=ntp state=installed"`

2) Playbooks
Modules can be called while writing task as
'Playbooks' using 'YAML'

**NOTE:** You do not need write module in Python only,
it can be written in other languages as long as
the format 'input & output' is written in a way that
ansible understands

### FINDING INFORMATION
```
ansible-doc --help
ansible-doc user | grep [Option]
ansible-doc -s user
```
### INVOKING A MODULE
`ansible [node] -s -m yum -a "name-vim state=present"`

**NOTE:** You must run these commands within the project folder

# Using Common Modules Labs

Lab 1 Solution
`ansible prod -m group -b -a 'name=admin state=present gid=7045'`

Lab 2 Solution
`ansible 'prod:!db' -m user -b -a 'name=abc state=present uid=7045 group=admin'`

Lab 3 Solution
`ansible app -m copy -a 'src=test.txt dest=/tmp/test.txt mode=0644'`

//Command Modules and Idempotence
//Using Ansible-Console REPL Shell

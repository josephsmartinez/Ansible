# YAML Primer

### YAML Primer
  - Begin / End Tags
  - List
  - Dictionaries
  - Indentation
  - Line Foldings

### Common YAML format
```
---
# This is a YAML Document
- list item 1
- list item 2
...
```

### List and Dictionaries
```
---
- name: configure app hosts
  host: app
  become: true
  tasks
    - package: name=apache state=present
    - copy: name=ntp.conf src=file/ntp.conf dest=/etc/ntp.conf
    - user: name=dojo state=present
...
```

## Styles: Line folding Vs Indentation
### Line Folding (Read the file as one line)
```
---
- name: configure app hosts
  host: app
  become: true
  tasks
    - package: name=apache state=present

    - copy: >
        name=ntp.conf
        src=file/ntp.conf
        dest=/etc/ntp.conf

    - user: |
        name=dojo
        uid=5001
        home=/home/dojo
        state=present
...
```
### Non-Line Folding
```
---
- name: configure app hosts
  host: app
  become: true
  tasks
    - package: name=apache state=present

    - copy:
        name=ntp.conf
        src=file/ntp.conf
        dest=/etc/ntp.conf

    - user:
        name=dojo
        uid=5001
        home=/home/dojo
        state=present
...
```

### EXAMPLE USING A SHOPPING LIST :)
```
---
- name: shopping list
  type: vegetables
  location: vegetables vendor outside hardware shop
  priority: 1
  items:
    - onions:
        size: small
        shape: round
        color: red
        qty: 1.5kg

    - apple:
        size: small
        color: green
        qty: 10
...
```
# Anatomy of a Playbook

### Plays Structure

- name
- hosts
- become
- vars
- task

```
---
name: App Server Configurations
  host: app
  become: true
  become_user: admin
  become_method: sudo
  vars:
    apache_port: 8080
    max_connection = 4000
    ntp_conf = /etc/ntp.conf
  task:
    - name: create app user
      user: name=app state=present uid=5002

    - name: install git
      yum: name=tree state=present
...
```

### Become
"think sudo"

supports `sudo, su, pfexec, doas, pbrun, dzdo, ksu` and others

### Tasks (Four Concepts to note)
"Components of Plays which define the 'desired state'
of action' on a system entity
"
"There is a 1-1 'mapping' between the task and the system entity managed"
"Task invoke 'modules' which are encapsulated procedures to take 'action'"
"'modules' are also called as 'task plugins'"

###Task Styles

Best practice is to provide documentation
```
- name: install ntp package
  yum:  name=ntp  state=present
```
Ambiguous task
```
- yum: name=ntp state=present
```
Multi Line Tasks (non YAML)
```
- name: create dojo user
  user: > or |
    name=dojo
    uid=5001
    home=/home/dojo
    state=present
```

Multi Line Tasks (YAML)
```
- name: create dojo user
  user:
    name: dojo
    uid: 5001
    home: /home/dojo
    state: present
```

# Writing a Playbook
PLEASE SEE LAB 2

# Validating, Troubleshooting, Applying Ansible Playbook

Command for testing and running **Playbooks**

Applying the playbook
- `ansible-playbook playbook.yml`

Dry Run
- `ansible-playbook playbook.yml --check`

Step Debugging
- `ansible-playbook playbook.yml --step`

Syntax Checking
- `ansible-playbook playbook.yml --syntax-check`

Playbook help
- `ansible-playbook --help`

List Host to which this playbook applies
- `ansible-playbook playbook.yml --list-host`

List Tasks
- `ansible-playbook playbook.yml --list-task`

List Tags
- `ansible-playbook playbook.yml --list-tag`

# Adding another play for app servers

Please review Lab3

# Nano Project: Create a playbook to deploy a static site

Please review Lab 4

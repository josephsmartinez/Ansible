## YAML Primer

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
## Anatomy of a Playbook

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



## Writing a Playbook




## Validating and Applying Ansible Playbook

## Troubleshooting Playbooks Failures

## Adding another play for app servers

## Nano Project: Create a playbook to deploy a static site

## Problem Statement

### Setup app Servers

Add a new play to existing playbook which will,
- create a **deploy** user with uid **5003**
- install **git**

on all **app** servers in the inventory

```
---
  - name: base systems configuration for linux servers
    hosts: prod
    become: true
    tasks:

      - name: create admin
        user:                 # Module
          name: admin
          state: present
          uid: 5001

      - name: remove user dojo id present
        user: >
          name=dojo
          state=absent

      - name: install tree
        yum: |
          name=tree
          state=present

      - name: install ntp
        yum:
          name: ntp
          state: installed

  - name: configuring app servers only
    hosts: app
    become: true
    gather_facts: false
    tasks:
      - name: create and deploy user
        user:
          name: deploy
          state: present

      - name: install git
        package:
          name: git
          state: installed
```

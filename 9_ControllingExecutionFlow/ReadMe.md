# Conditionals

## Overview of Iterators
```
tasks:
  - name: "shut down Debian flavored systems"
    command: /sbin/shutdown -t now
    when: ansible_os_family == "Debian"
    # note that Ansible facts and vars like ansible_os_family can be used
    # directly in conditionals without double curly braces
```
## Iterating over a list to install packages

Remember that the **systems** role gets called because it is a dependency within `/apache/meta/main.yml`


## Iterating over a dictionary to create users
Example of the iterating over dictionary of users  
Notice how the default values have been set in case
the variable data is not defined when iterating over the list   
roles/systems/task/main.yml  
```
---
# tasks file for systems
  - name: create system users
    user:
      name: "{{ item.key }}"
      uid: "{{ item.value.uid | default('none') }}"
      shell: "{{ item.value.shell | default('none') }}"
      home: "{{ item.value.home | default('none') }}"
      state: "{{ item.value.state | default('none') }}"
    with_dict: "{{ users }}"

  - name: install common system packages utilities
    package:
      name: "{{ item }}"
      state: installed
    with_items:
      - "{{ systems.packages }}"
```



## Using conditionals in task and templates
## Adding Ubuntu support by including vars
## Making application compatible with Ubuntu

Resources:
Conditionals    
https://docs.ansible.com/ansible/2.5/user_guide/playbooks_conditionals.html#applying-when-to-roles-imports-and-includes  

Loops  
https://docs.ansible.com/ansible/2.5/user_guide/playbooks_loops.html

Looping over Hashes
https://ansible-manual.readthedocs.io/en/latest/playbooks_loops.html

Defaulting Undefined Values
https://docs.ansible.com/ansible/2.5/user_guide/playbooks_filters.html#defaulting-undefined-variables

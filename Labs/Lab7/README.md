# Exercise
### System Roles and Sitewide Playbook
- Create a Systems Role for common tasks
- Move all task in the system.yml to this role
- Define role nesting with dependencies/meta-data
- Create Site Wide Playbook

After installing the roles "system"
We added the following within the main.yml task
```
---
# tasks file for system
    - name: create admin user
      user:
        name: admin
        uid: 5001
        shell : /bin/bash
        home : /home/admin
        state : present

    - name: remove user dojo
      user:
        name: dojo
        state: absent

    - name: install tree utility
      yum:
        name: tree
        state: present

    - name: install ntp
      yum:
        name: ntp
        state: installed
```
Next the dependency was added to apache
```
dependencies: [ system ]
  # List your role dependencies here, one per line. Be sure to remove the '[]' above,
  # if you add dependencies to this list.
```
Last we create site.yml at the root of the project folder
Here we used the `import_playbook` 
```
---
  - import_playbook: app.yml
```

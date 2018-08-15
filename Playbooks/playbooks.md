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
      - copy: name=ntp.conf src=file/ntp.conf destination
      - user: name=dojo state=present
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
      - copy: name=ntp.conf src=file/ntp.conf destination
      - user: name=dojo state=present
  ...
  ```

## Anatomy of a Playbook

## Writing a Playbook

## Validating and Applying Ansible Playbook

## Troubleshooting Playbooks Failures

## Adding another play for app servers

## Nano Project: Create a playbook to deploy a static site


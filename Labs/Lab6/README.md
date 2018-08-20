# Exercise
### Role to install PHP
- Create a **php** role
- Add task to install **php** and **php-mysql** packages
- Send a notification to restart apache after installing the packages

Start by create the scaffolding of the PHP module
```
ansible-galaxy --offline --init-path=roles php
```

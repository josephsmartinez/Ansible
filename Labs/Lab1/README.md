# Problem Statement 1

### Create a group
- on all prod servers
- whose name is 'admin'
- whose gid is '7045'
```
module:group
  name = admin
  state = present
  gid = 7045
```
# Problem Statement 2

### Create a user
- on all prod servers
- except of db hosts
- whose name is 'abc'
- whose uid is '7001'
- who belongs to 'admin' group
- who has a home directory
```
  module:user
    name = abc
    state = present
    uid = present
    group = admin
    host pattern ='prod:!db' #all nodes, just not database
```

# Problem Statement 3
### Copy a file
- whose name is 'test.txt'
- to all app servers
- at path /tmp/test.txt
- whose permission are set to 644
```
  module:copy
    src=test.txt
    dest=/tmp/test.txt
    mode=644
    host pattern=app
```

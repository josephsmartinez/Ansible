# AdHoc Command List

### IP discovering
`ansible -b -a "ifconfig" | less`

### Packages and Software

### Ports

### Operating Systems Family

### Mounts and Memory


# ANSIBLE ADHOC COMMANDS CHEATSHEET

# Checking Configurations
ansible-config dump

## GATHER RAW FACTS AND VARIABLE INFROMATION
ansible hostname -m setup

`ansible test -m setup -a "filter=ansible_fqdn gather_timeout=240 `
`ansible test -m setup -a "filter=ansible_os_family"  `

### TYPES OF FACTS
Printing all facts to a file
`ansible all -m setup -t outputfile.json`

## HOST PATTERNS
wildcards all, * , app*, *.example.com
hosts/groups app1, app1:app2, db, app:lb
subscripts `app[0], app[-1], prod[0:3], prod[2:]``
exclusion ! prod:!db
intersection ? prod:&app
regex ~ ~(app|db)*

The --limit option can be used along with ansible and playbook commands to restrict execution to specific set of host/groups --limit

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

## INVOKING A MODULES
Installing software
`ansible [node] -s -m yum -a "name-vim state=present"`

Update packages
`ansible [node] -m yum -a "name='*' state=latest"`

## INVOKING A MODULES USE TAGS
Running a job on one computer using tags and vars
`ansible-playbook playbooks/basemap.yml --tags "test_program" --extra-vars "variable_host=atmos-lab-pc2.panther.ad.fiu.edu"`


# Define host and variables assigned
castic_test --list


## Vars and Templates

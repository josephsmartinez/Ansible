# Ansible-cmdb | Fact gathering and converts it into a static HTML


Ansible-cmdb takes the output of Ansible's fact gathering and converts it into a static HTML overview page (and other things) containing system configuration information.  

## Full usage
```
Usage: ansible-cmdb [option] <dir> > output.html

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -t TEMPLATE, --template=TEMPLATE
                        Template to use. Default is 'html_fancy'
  -i INVENTORY, --inventory=INVENTORY
                        Inventory to read extra info from
  -f, --fact-cache      <dir> contains fact-cache files
  -p PARAMS, --params=PARAMS
                        Params to send to template
  -d, --debug           Show debug output
  -q, --quiet           Don't report warnings
  -c COLUMNS, --columns=COLUMNS
                        Show only given columns
  -C CUST_COLS, --cust-cols=CUST_COLS
                        Path to a custom columns definition file
  -l LIMIT, --limit=LIMIT
                        Limit hosts to pattern
  --exclude-cols=EXCLUDE_COLUMNS
                        Exclude cols from output
```
## Available templates
Ansible-cmdb currently provides the following templates out of the box:  
```
html_fancy: A dynamic, modern HTML page containing all hosts.
html_fancy_split: A dynamic, modern HTML page with each host's details in a separate file.
txt_table: A quick text table summary of the available hosts with some minimal information.
json: Dumps all hosts including groups, variable, custom info in JSON format.
csv: The CSV template outputs a CSV file of your hosts.
markdown: The Markdown template generates host information in the Markdown format.
sql: The SQL template generates an .sql file that can be loaded into an SQLite or MySQL database.
```


ansible-cmdb -t sql  /root/systemFacts_WebPage/  > host_fact.sql



https://ansible-cmdb.readthedocs.io/en/latest/

# Introduction to Ansible

    DevOps
    
    Manual -> SysAdmins
    Scipts -> IT Automantion
    IaaC   -> DevOps (Infrastructre as a Service)


    1960s - Mainframes
    1970s - Personal Computers
    1980s - Client Server
    1990s - Web Enterprises
    2000s - Cloud

    Configuration Management
        - Salt Stack
        - Chef 
        - Puppet

    Specialized deployment tools
        - Fabric
        - Capistrano
    
    Provisioning Tools
        - Terraform
        - Heat
        - Cloud Formation

    Ansible
    - Ad Hoc Server Management
    - Configuration Management
    - Deployment and Orchestration
    - Provisioning
    - Deferent play books can be applied to the same set of nodes, where puppet dose not such flexability to change the state the node once defined. 
    
    Simple and uses YAML and Python
    
    Agent Less (Push Model)
    - Uses SSH / WinRM
    - Simple to Setup
    - Smaller Footprint
    
    Push Model
    - Lets you control the sequence of pushing
    - Ability to define the orchestration
    - Not as flexable as a pull model
    - Extenable with Python and Shell Scripts
    
    Batteries Included
    - Models let you interact with the system without downloading 
    - Many tools come with Ansible for fast set up
        - System
        - Networking
        - Cloud
        - Monitoring Tools
        - Containers
        - Collaboration Tools
        - Source Control

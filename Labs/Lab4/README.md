# Problem Statement
## Nano Project 1: Deploy a static html site
---
### Create a Playbook website.yml with the following
Specifications:

- It should apply only on **lb (load balancers)** host
- Should use **become** method
- Should add a repository (yum_repository) for nginx
with `gpgcheck=no and baseurl=http://nginx.org/packages/centos/6/x86_64/`
- Should install and **nginx** service
- Should install **git**
- Should deploy a sample html app into the default web root directory of nginx using ansible's got module.
  - Soure repo: https://github.com/schoolofdeveops/html-sample-app.git
  - Deploy Path: /usr/share/nginx/html/app
- Once deployed, validate the site by visiting
http://codebox_ip:8080/app (8000)

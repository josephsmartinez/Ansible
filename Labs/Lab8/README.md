# Exercise
## Nano Project: Deploy a PHP Application
DevOps-demo-app is an application written in PHP. You have already setup the environment above with apache and php roles, to deploy this application. Your job is to write the ansible code to deploy this application on app servers. This code will be in the form of a role.

### You have been tasked to create a froentend role with the following specs,

- Pull release packages from the github release page as provided in the resources below. Releases are in the form of an archive.

- Multiple copies of releases will be maintained on the app servers for enabling rollbacks. To support this, every time to deploy a new version of the app, create a new directory for it inside the /opt/app

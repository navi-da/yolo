# Explain each role's function and positioning in the playbook (since a playbook is run sequentially) and the Ansible modules applied in the tasks contained within the roles
## Roles functions and positioning
The playbook is divided into the folllowing roles. The roles are run in the following order to build dependancies for the next role
**git**
Updates the apt cache and installs git. In addtition, it clones the repo to the devops folder in the vagrant box
**docker**
Installs docker
**docker_network**
Sets up the docker network
**docker_volume**
Sets up the docker volume
**database**
Pulls and builds the database container
**frontend**
Pulls and builds the client container
**backend**
Pulls and builds the backend container

## Ansible modules used
**apt**:to install packages
**git**:to clone the repo
**docker_network**:to create the docker network
**docker_volume**:to create the docker volume
**docker_container**:to setup and start the containers
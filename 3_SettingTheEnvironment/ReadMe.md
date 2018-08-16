# Setting up the environment
Code Space IO

## Docker Commands

### Digital Ocean
https://github.com/codespaces-io/codespaces

### Start Containers
`docker-compose up -d`

### Stop all container
`docker-compose stop`

### Starting -> Stopping -> Removing Nodes
- `docker-compose up -p [node name]`

- `docker-compose stop -p [node name]`

- `docker-compose rm [node name]`

### Stop and removal all node
- `docker-compose down`

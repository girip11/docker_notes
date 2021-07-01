# Docker Useful commands for development

```Bash
#1. To launch terminal on the container
docker container exec -it container_name bash

# 2. run the docker container in debug mode
# service_name can be found in the docker-compose.yml
docker-compose run --service-ports service_name

# 3. build the docker container
docker container build -t image_name:tag_name .
# build the entire service
docker-compose build

# 4. start the services locally
# -d to launch the services in the background
docker-compose up [-d]

# 5. To check all the running containers
# -a - to list all containers including the exited ones
docker container ls [-a]
# to see all the containers of current service
docker-compose ps [-a]

# 6. stop services. -v to remove the volumes as well
docker-compose down [-v]

# 7. Remove a specific container which is stopped
# -f - to force remove a running container
docker container rm [-f] container_name
# if the container is running either we can force remove or kill and remove
docker container [stop|kill] container_name \
&& docker container rm container_name

# 8. List all docker images
docker images
docker image ls

# 9. Pruning images
docker image prune -F
# pruning stopped containers, unused networks,
# build cache and dangling images
docker system prune
```

---

## References

* [Docker useful commands for development](https://dev.to/aduranil/10-docker-compose-and-docker-commands-that-are-useful-for-active-development-22f9)

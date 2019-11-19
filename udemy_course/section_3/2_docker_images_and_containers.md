# Docker images and containers

* Image - consist of all the resources/artifacts that make up the application.
* Container - running instance of the image. Many containers of the same docker image can run simulatneously.
* Docker hub - Docker's default image registry. Consider it as a repository of docker images.

## Docker container management commands

### Launching a docker container

Example: Launching nginx web server.

~~~bash
# runs in the foreground
# everytime this command is run, it spawn a new container
docker container run --publish 80:80 nginx

# to spawn the container in the background use --detach option
docker container run --publish 80:80 --detach nginx

# Launching a container with user defined name
# Any other container running or stopped should not have this name
docker container run --publish 80:80 --detach --name webserver nginx
~~~

* Docker engine searches for image **nginx** in the local image cache. If the image is not available, pulls the latest image(by default) from default docker registry which is the docker hub. Explicit version/tag of the image to be downloaded can also be specified.

* Once the image is downloaded, a new container is launched.

* Assigns a virtual IP on a private network managed by the docker engine.

* `--publish 80:80` - does a port mapping of host OS to the docker container. When the http requests hits the host on port 80, the traffic will be forwarded to the docker container on its port 80.

* Starts the container by using the **CMD** present in the image **Dockerfile**

### Listing the containers

~~~bash
# lists all the images in the local cache
docker image ls

# old
docker ps

# new
# show by default only the running containers
docker container ls

# to list even the exited containers
docker container ls -a
~~~

We can get the container ID from the above commands.

### Starting and Stopping the container

~~~bash
# CONTAINER_ID and CONTAINER_NAME can be obtained from `docker container ls -a`
docker container stop <CONTAINER_ID | CONTAINER_NAME>

docker container start <CONTAINER_ID | CONTAINER_NAME>
~~~

### Accessing logs of the container

~~~bash
# old way
docker logs <CONTAINER_ID | CONTAINER_NAME>

# new way
docker container logs <CONTAINER_ID | CONTAINER_NAME>
~~~

### List processess of a docker container

~~~bash
# old style
docker top <CONTAINER_ID | CONTAINER_NAME>

# container processes will also be visible on the docker host
docker container top <CONTAINER_ID | CONTAINER_NAME>

# webserver being the name of the container
docker container top webserver

# from the above results, catch a keyword like nginx or the PID
#  and search using pgrep on the docker host
# `pgrep -af nginx` for example
~~~

### Deleting the containers

Once all the containers are deleted, `docker container ls -a` returns no results.

~~~bash
# old style
# can give multiple container id or name each space separated
docker rm <CONTAINER_ID | CONTAINER_NAME>

# new style
# below command removes only the exited containers
# can give multiple container id or name each space separated
docker container rm <CONTAINER_ID | CONTAINER_NAME>

# to remove all the containers including those in the running state
# can give multiple container id or name each space separated
docker container rm -f <CONTAINER_ID | CONTAINER_NAME>
~~~

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)

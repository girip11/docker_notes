# Shell inside container

## `run` command

~~~bash
docker container run --help

# option t - pseudo tty
# option i - interactive
# open bash shell inside container
# starts a container from nginx image but with bash shell
# command will override dockerfile command
# docker container run -it --name [container_name] [image_name] [command] [args]

# launches minimal version of ubuntu as docker image and starts an interactive bash terminal
docker container run -it --name ubuntu ubuntu bash

# use --rm to remove the container as soon as the container exits
docker container run --rm -it --name ubuntu ubuntu bash

# exiting the bash shell stops the container.
docker container ls -a

# start the same container in to interactive mode
# docker container start --help
# docker container start -ai [CONTAINER_NAME]
docker container start -ai ubuntu

# Inside this bash shell of ubuntu container, can install
# any other software using the apt package
apt --help

# This will be installed only for that container instance.
# another container spawned from same image will not have curl installed
apt install -y curl
~~~

**NOTE**: Changes made to a container for example by installing a software inside a container, affects only that container. A new container spawned from the same image will not have those installed packages.

## `exec` command

* `docker container exec --help` - helps run a command inside a **running container**

~~~bash
# start a nginx container in the background
docker container run -p 80:80 -d --name webserver nginx

# verify its in running state
docker container ls | grep webserver

# docker container exec -it [container_name] command args
# launch bash shell inside the running container
docker container exec -it webserver bash

# ps command might not be found on nginx container
# install ps
apt update && apt install -y procps

# lists all processes running inside the container
ps aux

# exits bash shell. Does not exit the container
exit

# check if nginx container is still running
docker container ls
~~~

**NOTE**: Alpine is a very small (~5MB) **security focusses** linux distribution. It is considered ideal for container images. Alpine image does not ship with bash. Just ships with **sh**. Bash can be installed using alpine's package manager **apk**

~~~bash
docker pull alpine

# see the image size compared to ubuntu
docker image ls

docker container run -it --name alpine alpine sh

# apk is the package manager
apk --version
~~~

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)

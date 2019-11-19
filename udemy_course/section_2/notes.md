# Chapter 2

* [Docker playground](play-with-docker.com)

## Installation on different platforms

* Windows 10 Pro/Ent installation. Older windows versions docker installtion using **docker toolbox**.

* Docker setup on Mac

* Installation on Linux. [Docker Debian installation](https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/debian/#set-up-the-repository)

* Docker requires root permissions to talk to docker daemon. Add the required user to the `docker` group.

```bash
# checking docker installation
docker version
# docker versions are in YY.MM format (year and month)
```

## Docker machine

> Docker Machine is a tool that lets you install Docker Engine on virtual hosts, and manage the hosts with docker-machine commands - [Docker machine](https://docs.docker.com/machine/overview/)

* [Install docker-machine](https://docs.docker.com/machine/install-machine/)
* This will be required for using with docker swarm.

## Docker compose

> Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services - [Docker compose](https://docs.docker.com/compose/)

* [Install docker-compose](https://docs.docker.com/compose/install/)

## Editor

* Install Visual studio code (VSCode).
* Install [**docker plugin**](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)

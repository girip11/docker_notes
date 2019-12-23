# Inspecting containers

## `top` command

* Lists processes inside a container

~~~bash
docker container top <CONTAINER[Id|Name]>
~~~

## `inspect` command

* Details about the container like netwroking, host port mapping etc. Returns a JSON.

~~~bash
docker container inspect <CONTAINER[Id|Name]>
~~~

## `stats` command

* Returns statistics like cpu, memory, network, disk etc usage of a docker container

~~~bash
docker container stats --help

# stats of all running containers
docker container stats

# stats of all containers in any state
docker container stats -a

# stats for a specific container
docker container stats webserver
~~~

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
* [docker container inspect reference](https://docs.docker.com/engine/reference/commandline/inspect/)
* [Docker inspect template magic](https://blog.container-solutions.com/docker-inspect-template-magic)

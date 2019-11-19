# Docker networking

## Docker host container port mapping

* Whenever container needs to receive external requests, there needs to be a host to container port mapping.

* When a port mapping is created, a firewall exception for the host port is created for receiving inbound traffic on that port so that the requests can be forwarded to the container.

* Docker container and host belong to different networks. Host forwards the traffic to the bridge network and from there the request reaches the docker container.

* Docker containers communicate over a virtual network(bridged network) created and managed by the docker engine within a host. For instance, **container** running a http server and another container running a **database server** can communicate with each other without any port mapping as long as they are in the same virtual network.

* This port mapping also helps avoid port conflict by allowing any host port to be mapping to same port on different containers.

* Create bridge network within smae docker host and connect all containers to that bridge network so that those containers can communicate with each other.

~~~bash
# forward requests hitting host port 80 to container's port 80.
docker container run -d -p 80:80 --name nginx nginx

# docker container port
docker container port nginx

# docker container ip addres
# format follows JSON tree structure
# GO template
docker container inspect --format "{{ .NetworkSettings.IPAddress }}" nginx
# or
docker container inspect nginx | grep IPAddress

# host ip address
ifconfig
~~~

## Docker network management

`docker network --help`

### List docker networks

~~~bash
# lists all docker networks
# default we have three networks bridge, host and none
# bridge - bridge driver (default)
# host - host driver. Container directly becoming part of host network. Improves performances(NO NAT?), but with security concerns
# none - no driver
docker network ls
~~~

### Inspecting a network

~~~bash
# IP address range of the network
# see containers attached to a network
docker network inspect bridge
docker network inspect host
docker network inspect none
~~~

### Creating a docker network

`docker network create --help`

~~~bash
# create a bridge network
docker network create my_app_net

docker network ls

# attaching a new container to a network
docker container run -d -p 80:80 --name webserver --network my_app_net nginx

# check if the container is attached to this network
docker network inspect my_app_net
~~~

### Connecting a container to a docker network

* Equivalent of adding another NIC to the docker container.
* `docker network connect --help`
* Automatic IP address assignment can be done. Static ip assignment can be done using the **ip** option.

~~~bash
docker container run -d -p 80:80 --name webserver nginx

# docker network connec [network_name_or_id] [container_name_or_id]
docker network connect my_app_net webserver

# this container is now part of
# default bridge network and my_app_net network
docker container inspect webserver

docker network inspect my_app_net
~~~

### Disconnecting a container from a docker network

* Removes the docker container from a given docker network.
* `docker network disconnect --help`

~~~bash
docker network disconnect my_app_net webserver

# verify the network disconnect from container and network info
docker container inspect webserver

docker network inspect my_app_net
~~~

### Deleting a docker network

`docker network rm --help`

~~~bash
# get the name of the network to delete using below command
docker network ls

docker network rm [network_name_or_id]
~~~

### Delete unused docker networks using `prune`

`docker network prune --help`

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)

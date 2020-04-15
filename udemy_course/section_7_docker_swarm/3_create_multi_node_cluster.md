# 3 Node swarm setup

* Use `labs.play-with-docker.com` - setup resets after 4 hours. Browser required.
* Using **docker-machine** (needs to be [installed separately](https://docs.docker.com/machine/install-machine/))and **virtualbox**. Tutorial on creating a swarm cluster using docker machine can be found [here](https://www.melvinvivas.com/create-a-swarm-cluster-using-docker-machine/)

* management commands wont work on worker nodes.

```Bash
# To create a node using busybox linux distro
docker-machine create node1

# SSH access
docker-machine ssh node1

# sets ENV on the current terminal
# so that all docker commands are sent to the
# daemon running as pointed by the DOCKER_HOST env
eval $(docker-machine env node1)

# check which daemon/engine the CLI is pointing to
docker info
```

* Add a worker as manager. This command can be executed only on a manager node.

```Bash
# add a node to swarm cluster using swarm join

# list the manager nodes
docker node ls

# Add a worker as manager
docker node update --role manager <node_name>
```

* `docker swarm join-token manager` - gives the token/command needed to join a machine to the swarm cluster as a **manager**.

* `docker swarm join-token worker` - gives the token/command needed to join a machine to the swarm cluster as a **worker**.

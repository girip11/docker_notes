# Create swarm service

* `docker swarm init` does the following things

* `docker swarm --help` - more on the swarm command. Helps to create a swarm, add and remove nodes to/from swarm.

* root signing certificate for the swarm
* Certificate for the first manager node. (All managers communicate over a secure channel)
* Generate join token

* Raft database is created. This database stores the root CA, configuration and secrets. This database will be replicated to every manager node.

* Raft database is stored encrypted on the disk.

## Manager nodes

* `docker node --help` - With the node command we can **add**, **remove** nodes from swarm, **promote** or **demote** worker to/from manager

* There can only be **one leader node** among many manager nodes

```Bash
# Lists all the nodes in the swarm cluster
docker node ls
```

## Manage services

* A service can have replicas. Number of replicas for a service equals the numbers of containers that service is running on.

* `docker service --help` - create, list, remove, scale services.  

```Bash
# creates a service in swarm
docker service create alpine ping 8.8.8.8

# list the running services
docker service ls

# To list the containers associated with a service
docker service ps <service_name>

# To scale a service
docker service update <serivce_id_or_name> --replicas 3
```

* `docker update --help` - alter resource usage of containers.

* `docker service scale ---help` - can be used for scaling the multiple services

* `docker service logs --help` - access the service logs. We can also see the logs from a particular replica in the service.

* `docker service inspect <service_name>` - inspect services

* When one of the replica container dies/removed, swarm notices this and relaunches/recreates the replica maintaining the replica count.

* `docker service ps <service_name>` - list all the container creation, deletion history.

* `docker service rm <service_name>`

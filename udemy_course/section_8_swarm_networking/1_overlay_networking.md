# Swarm overlay networking

* `docker network create --driver overlay <network_name>`

* Overlay network - like Virtual LAN. Swarm wide bridge network. This is used for intra swarm communication.

* IPSec can be enabled in overlay networks. Disabled by default.

* A service can be connected to multiple overlay networks (similar to a node having multiple NIC and each NIC is connected to a different network)

```Bash
docker network create --driver overlay myoverlay

docker service create --name psql --network myoverlay  -e POSTGRES_PASSWORD=MyPassw0rd postgres

docker service ls

# watch command runs the command repeatedly
watch docker service ls

docker service ps psql
```

* Services communicate with each other using the **service names**

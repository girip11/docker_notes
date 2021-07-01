# Swarm

* clustering solution - groups hosts to orchestrate container lifecycle

* Manager and worker nodes.

* Graph database stores the configuration and is replicated on all manager nodes.

* Manager notes communicate with each other over secure network(encrypted traffic)

* Manager nodes each contain an internal datastore called as **raft**

* Worker nodes where the containers will be launched.

* Worker nodes will be communicating with master nodes to get the tasks(A task is usually a spin up of a container).

* By default, swarm is not enabled

```bash
# prints **Swarm: inactive**
docker info | grep -i swarm
```

* By default docker swarm tries to spread out the replicas.

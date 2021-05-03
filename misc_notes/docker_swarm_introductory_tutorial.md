# Docker swarm tutorial

This series is a great resource on learning about the docker swarm. This series can be thought of as a nice introductory tutorial to docker swarm.

**NOTE**- I have stored these articles in my **POCKET library**

## Key learnings

- Global vs replicated mode. Global exactly one task per schedulable node for the service. Replicas allows services to be scaled horizontally.

- Spread scheduling strategy.

- Placement constraints

- Placement constraints vs placement preferences. Official documentation details can be found [here](https://docs.docker.com/engine/swarm/services/) under the placement preferences section.

- Swarm tries to main the desired state configuration. Hence it will reschedule tasks when tasks or the nodes fail and sufficient resources are available on the remaining nodes in the cluster. Else the tasks that cannot be scheduled will be marked as pending till resources are available.

> Each Docker engine runs an embedded DNS server, which can be queried by processes running in containers on a specific Docker host, provided that the containers are attached to user-defined networks (i.e. Note: not the default bridge network, called bridge). Container and Swarm service names can be resolved using the embedded DNS server, provided the query comes from a container attached to the same network as the container or service being looked up. In other words, name resolution is network scoped, and generally speaking, networks are isolated from each other. However,this does not preclude containers or services being attached to more than one network at a time.

- Docker engine's embedded DNS Server.

- Swarm's inbuilt Layer 4 load balancing and routing mesh.

**NOTE**- Placement preferences are ignored for global mode services.

## CPU management in docker

---

## References

- [Part-1: Bootstrapping a Docker Swarm Mode Cluster](https://semaphoreci.com/community/tutorials/bootstrapping-a-docker-swarm-mode-cluster)
- [Part-2: Scheduling Services on a Docker Swarm Mode Cluster](https://semaphoreci.com/community/tutorials/scheduling-services-on-a-docker-swarm-mode-cluster)
- [Part-3: Consuming Services in a Docker Swarm Mode Cluster](https://semaphoreci.com/community/tutorials/consuming-services-in-a-docker-swarm-mode-cluster)
- [CPU management in docker](https://www.docker.com/blog/cpu-management-docker-1-13/)

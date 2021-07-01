# Routing Mesh

* routing mesh is an ingress network that distributes packets for a service to its tasks(containers)

* This mesh span across all the nodes. Uses the IPVS from linux kernel

* Builtin load balancing for a service across its replicas.

* Service name by default acts as the DNS name. Virtual IP(VIP) assigned to every service DNS name. Within an overlay network, container to container communication happens through the service name which resolves to the VIP. Once the packet is targeted to the VIP, swarm does the load balancing across the service replicas.

* Every node contains a builtin load balancer listening on the public IP address and listens on all the published ports from all the services.

* In swarm, even though the service might not be running on all the nodes in the cluster, every node would be listening on the published ports of the service. External traffic can hit any of the worker nodes, but still will be routed to one of the nodes where the service replicas are running.

* Routing mesh and load balancing are stateless.

* Load balancer operates at the Transport layer(TCP stack) and not at the application layer (like nginx)

* If we need application layer load balancing we can use nginx or HAProxy

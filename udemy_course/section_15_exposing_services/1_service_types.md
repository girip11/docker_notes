# Exposing containers

- `kubectl expose` creates a service for existing pods.
- A service is a stable address for accessing pods
- **CoreDNS** allows resolution of services by name

Different types of services

- Cluster IP (default)
- Node Port
- Load Balancer
- External Name

## ClusterIP

- Default mechanism
- Available(reachable) only within the cluster
- Communication between Pods
- Single internal virtual IP allocated.
- Pods can reach service on the apps port number

## Node Port

- Outside entities to communicate with the pods
- High port(not well known ports) allocated on each node.
- Port is open on every node's IP
- Anyone able to reach the node, can connect via its IP and port

The above two types are available in the kubernetes out of the box.

## Load balancer

- Cloud solutions. Load balancers in the cloud offering will be configured to send the traffic to NodePort, creates nodeport + ClusterIP services.

## External Name

- This is for pods to communicate with the external services via DNS.
- Adds CNAME DNS record to the core DNS for name resolution.
- Usecase - If we want to route to a service internal to the cluster but with an external DNS name(service migration to kubernetes scenario)

Kubernetes Ingress for HTTP traffic

# Exposing service via Port

- `kubectl expose deployment <name> --port <port>` creates a clusterIP for the service.
- This clusterIP can be obtained by running `kubectl get service`

- Either we can reach to the service via the `ClusterIP:port` combination when outside the cluster node but still reachable to the node.
- If we are inside of pods in the cluster, we can access the service via the deployment name

## Creating node port

- Creating node port also creates a new cluster IP.

```bash
# This also creates a cluster IP inaddition to exposing a port on the node
kubectl expose deployment httpenv --port 8888 --name httpenv-np --type NodePort
```

This creates another service which can be listed using `kubectl get service`.

- ClusterIP that's created during creation of node port will be bound to the **port 8888** in the above example.

- From the linux host(when its a cluster, from inside the node), we can do `curl 127.0.0.1:<node_port>`. Get the node port from `kubectl get service` command.

## With external load balancers

- We might need to install plugins to talk to external load balancers on cloud.

- Creating load balancer endpoint, creates a cluster IP as well as node port.

```bash
kubectl expose deployment httpenv --port 8888 --name httpenv-lb --type LoadBalancer
```

**NOTE** - status of the external IP for loadbalancer under `kubectl get service` is **PENDING** in kubeadm, minikube, microk8s. This is because there is no builtin LB with these distributions.

- Load balancer accepts the packet (load balancer backend forwarding), forwards to nodeport (node IP and assigned high port) which then forwards to the clusterIP and port.

## Deleting exposed ports/services

```bash
kubectl delete service httpenv httpenv-lb httpenv-np
kubeclt get service
```

---

## References

- [Using a Service to Expose Your App](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/)
- [Service](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Node port](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)

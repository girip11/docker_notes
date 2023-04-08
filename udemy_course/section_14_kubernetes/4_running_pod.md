# Running Pod with Kubectl

```bash
kubectl version
kubectl version --short

# Create and run a pod
kubectl run nginx-server --image nginx:1.23-alpine

# list replication controllers
kubectl get rc

# List all services
kubectl get services

# get all running pods
kubectl get pods

# get all running pods and services
kubectl get pods,services

# get all objects per namespace
kubectl get all

# All namespace resources
kubectl get all --all-namespaces

# all resources of a given namespace
kubectl get all -n kube-system
```

---

## References

- [Kubectl cheatsheet1](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Kubectl cheatsheet2](https://cheatography.com/gauravpandey44/cheat-sheets/kubernetes-k8s/)
- [Kubectl for docker users](https://kubernetes.io/docs/reference/kubectl/docker-cli-to-kubectl/)
- [Kubernetes architecture](https://cheatography.com/gauravpandey44/cheat-sheets/kubernetes-k8s/)

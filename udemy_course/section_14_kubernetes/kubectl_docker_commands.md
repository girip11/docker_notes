# Kubectl for docker users

- Docker command to run nginx container

```bash
docker run -d --restart=always -e DOMAIN=cluster \
--name nginx-app -p 80:80 nginx
```

Equivalent commands in Kubernetes

```bash
# deployment by default runs in the background
# like docker run -d
kubectl create deployment --image=nginx nginx-app

# set environment variable
kubectll set env deployment/nginx-app DOMAIN=cluster

# expose port
kubectl expose deployment nginx-app --port=80 --name=nginx-http
```

- To run in the foreground we need to use `kubectl run --rm -i -t --attach <name> --image=<image> --restart=Never`

```bash
# running bash shell
kubectl run --rm -i -t --attach python-shell \
--image=python:3.9-slim --restart=Never --command bash
```

- Attach to a running pod using `kubectl attach`

```bash
kubectl attach -it <pod_name>
```

- Execute a command on running pod using `kubectl exec <podname> -- <command>`

```bash
# Execute one of comands
kubectl exec nginx-server -- cat /etc/hostname

# Interactive exec
kubectl exec -it nginx-server -- /bin/sh
```

- Pod logs. Each pod run produces separate logs.

```bash
kubectl logs -f nginx-server

# Fetch the logs of the previous pod run.
kubectl logs --previous nginx-server
```

- Remove pod

```bash
kubectl get pod nginx-server

# Always delete the deployment that owns the pod and not the pod
# directly. When pod is directly deleted without deleting the deployment
# the pod is recreated
kubectl delete pod nginx-server
```

- Remove pod when deployed using deployment

```bash
kubectl get deployment nginx-server

# Always delete the deployment that owns the pod and not the pod
# directly. When pod is directly deleted without deleting the deployment
# the pod is recreated
kubectl delete deployment nginx-server
```

## Kubernetes version and info

```bash
kubectl version
kubectl cluster-info
```

---

## References

- [kubectl for Docker Users](https://kubernetes.io/docs/reference/kubectl/docker-cli-to-kubectl/)

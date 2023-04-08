# Creating deployment

```bash
kubectl create deployment nginx-server --image=nginx:1.23-alpine
```

## What happens while creating a deployment

- Kubectl client sends request to API server to create deployment, which then stores the data in the `etcd` store.
- Controller manager finds new deployment resource, then the deployment controller, replication controller will start to use this.
- Each deployment creates a replicaset which then creates the pods(staging/prod). For instance, we change the image version with the same deployment name, then a new replicaset for the same deployment is created and it will have its own set of pods. Thus replicasets serve as versioning of the deployment(staging/production).
- Controller manager(deployment controller) creates record for the replicaset after seeing deployment resource in the `etcd` store, the replication controller on seeing the replicaset, creates the pods in the `etcd` store. Scheduler will then work on this data.

```bash
kubectl delete deployment nginx-server
```

## Scaling replicasets

```bash
kubectl create deployment apache-server --image httpd:2.4-alpine
```

To scale a deployment, following command is used.

```bash
kubectl scale deployment apache-server --replicas 2
# or
kubectl scale deploy apache-server --replicas 2
```

- Scale command changes the deployment record. Controller manager recognizes that the replicas count changed. Then it edits the replicaSet to reflect this change(adds additional pods in case of scaling up). Scheduler assigns node to newly requested pods. Once node is assigned, kubelet in that node, communicates with the container runtime to start the pod(containers)

## Creating deployment with custom command

- `Kubectl run` is only used to start a pod. `kubectl create deployment` is used to create deployments

```bash
# custom command is prefixed with `--`
kubectl create deployment pingpong --image alpine -- ping 1.1.1.1
```

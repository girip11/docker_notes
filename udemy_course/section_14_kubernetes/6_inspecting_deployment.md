# Inspecting deployment objects

## Inspecting logs

```bash
# fetch all pods, replicasets, deployments
kubectl get all

# we can fetch logs of a particular pod
kubectl logs pod/apache-server-86bf65445-vxf8r

# logs of a deployment
kubectl logs deployments/apache-server --follow --tail 1

# Fetch the labels of pods using the below command
kubectl describe pod/apache-server-86bf65445-vxf8r

# Inspecting a deployment
kubectl describe deployments/apache-server

# get all pods based on a label
# It can pull the logs of up to 5 pods at a time using this label selector
kubectl logs -l app=apache-server
```

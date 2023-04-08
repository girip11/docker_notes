# Kubernetes DNS

- Host name access works only within the same namespace.

```bash
# List all available namespaces
kubectl get namespaces
```

- Services have a FQDN which is of the format `<hostname>.<namespace>.svc.cluster.local`. This DNS will resolve only within the cluster.

---

## References

- [CoreDNS plugin](https://coredns.io/plugins/kubernetes/)

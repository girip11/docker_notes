# Installation

- Easiest way is to enable kubernetes using docker desktop.
- On Linux host or VM we can use [**microk8s**](https://github.com/canonical/microk8s) to install kubernetes.
- K8s in a browser
  - [Play with K8s](https://labs.play-with-k8s.com/)

## Install microk8s

- Installed using snap from snap store.

```bash
snap install microk8s --classic
# Add the current user to this group to avoid prefixing commands with sudo
sudo usermod -a -G microk8s <username>

sudo chown -R girish ~/.kube
```

- Installs kubernetes without docker
- Control the microk8s service via `microk8s` commands
- Kubectl accessible via `microk8s kubectl`. Setup the alias `alias kubectl=microk8s kubectl`

```bash
microk8s kubectl get nodes
microk8s kubectl get services

microk8s status # enables, disabled and available addons

# additional services can be enabled using
microk8s enable dns
microk8s enable dashboard
```

- [Kubectl can be installed separately](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) and used with microk8s.

By default microk8s uses **containerd**. To switch to using docker as the container runtime, [following steps are required](https://stackoverflow.com/a/69732457)

- Edit **/var/snap/microk8s/current/args/kubelet** by changing `--container-runtime=docker`
- Stop and start the cluster using `microk8s stop` and `microk8s start`

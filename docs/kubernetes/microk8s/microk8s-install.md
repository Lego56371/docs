# Micro K8s Install Guide

1. Install MicroK8s on Linux
```bash
sudo snap install microk8s --classic
```

2. Check the status while Kubernetes starts
```bash
microk8s status --wait-ready
```

3. Turn on the services you want
```bash


microk8s enable dashboard

microk8s enable dns

microk8s enable registry

microk8s enable istio

```

4. Start using Kubernetes
```bash
microk8s kubectl get all --all-namespaces
```

5. Access the Kubernetes dashboard
```bash
microk8s dashboard-proxy
```
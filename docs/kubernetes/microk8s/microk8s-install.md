# Micro K8s Install Guide

1. Install MicroK8s on Linux
```bash
sudo snap install microk8s --classic
```

2. Check the status while Kubernetes starts
```bash
sudo microk8s status --wait-ready
```

3. Turn on the services you want
```bash


sudo microk8s enable dashboard

sudo microk8s enable dns

sudo microk8s enable registry

sudo microk8s enable istio

```

4. Start using Kubernetes
```bash
sudo microk8s kubectl get all --all-namespaces
```

5. Access the Kubernetes dashboard
```bash
sudo microk8s dashboard-proxy
```
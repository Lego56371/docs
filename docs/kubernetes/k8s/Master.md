# k8s Kubernetes Master Server Node

To setup a master server node follow the following steps

1. Download the latest release with the command
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

2. Install kubectl
```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

3. Test to ensure the version you installed is up-to-date:
```bash
kubectl version --client
```
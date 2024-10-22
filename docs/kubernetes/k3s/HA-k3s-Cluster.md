# High Availability k3s Cluster

Run this command on server-1
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=SECRET sh -s - server \
    --cluster-init \
    --tls-san=10.0.0.201 # Optional, needed if using a fixed registration address
```

Run this command on the server-2
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=SECRET sh -s - server \
    --server https://10.0.0.201:6443 \
    --tls-san=10.0.0.199 # Optional, needed if using a fixed registration address
```

Run this command on server-3
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=SECRET sh -s - server \
    --server https://10.0.0.201:6443 \
    --tls-san=10.0.0.200 # Optional, needed if using a fixed registration address
```
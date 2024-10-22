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


Edit this file on loadbalancer-1 and 2 /etc/haproxy/haproxy.cfg
```cfg
frontend k3s-frontend
    bind *:6443
    mode tcp
    option tcplog
    default_backend k3s-backend

backend k3s-backend
    mode tcp
    option tcp-check
    balance roundrobin
    default-server inter 10s downinter 5s
    server server-1 10.0.0.201:6443 check
    server server-2 10.0.0.199.51:6443 check
    server server-3 10.0.0.200:6443 check
```
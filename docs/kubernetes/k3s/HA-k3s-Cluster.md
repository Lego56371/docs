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


Edit this file on loadbalancer-1 and 2 '/etc/haproxy/haproxy.cfg'
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

Add the following to this file '/etc/keepalived/keepalived.conf' on both loadbalancers as well
```conf
global_defs {
  enable_script_security
  script_user root
}

vrrp_script chk_haproxy {
    script 'killall -0 haproxy' # faster than pidof
    interval 2
}

vrrp_instance haproxy-vip {
    interface eth1
    state <STATE> # MASTER on lb-1, BACKUP on lb-2
    priority <PRIORITY> # 200 on lb-1, 100 on lb-2

    virtual_router_id 51

    virtual_ipaddress {
        10.0.3.1/24
    }

    track_script {
        chk_haproxy
    }
}
```

Run this script on the agents
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=SECRET sh -s - agent --server https://10.0.0.203:6443
```
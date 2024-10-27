# High Availability Embedded etcd

First we need to setup the master server. To do this we run the following command. Replace the `<FIXED_IP>` with the ip address of that server
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=GFaA6OeUQOHPxgk8AIVltWu79X8jaxpfPhFzaJ5KlRQycYtY1xX6Ubepma sh -s - server \
    --cluster-init \
    --tls-san=<FIXED_IP> # Optional, needed if using a fixed registration address
```

Next we need to setup the 2 other servers to do that we run this command. Replace the `<MASTER-IP>` with the ip address of the master server and replace the `<FIXED_IP>` with the ip address of the server you are setting up
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=GFaA6OeUQOHPxgk8AIVltWu79X8jaxpfPhFzaJ5KlRQycYtY1xX6Ubepma sh -s - server \
    --server https://10.0.0.206:6443 \
    --tls-san=<FIXED_IP> # Optional, needed if using a fixed registration address
```

Run this command on the Agents
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=GFaA6OeUQOHPxgk8AIVltWu79X8jaxpfPhFzaJ5KlRQycYtY1xX6Ubepma sh -s - agent --server https://10.0.0.206:6443
```
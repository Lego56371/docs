# Nextcloud

### Install

1.  Once Docker is installed run this script

```bash
curl -fsSL https://get.docker.com | sudo sh
```

2. Once that is done run this command

```bash
# For Linux and without a web server or reverse proxy (like Apache, Nginx, Caddy, Cloudflare Tunnel and else) already in place:
sudo docker run \
--init \
--sig-proxy=false \
--name nextcloud-aio-mastercontainer \
--restart always \
--publish 80:80 \
--publish 8080:8080 \
--publish 8443:8443 \
--volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config \
--volume /var/run/docker.sock:/var/run/docker.sock:ro \
nextcloud/all-in-one:latest
```

3. After that you open up your web browser and go to this address

https://ip-address:8080


<details>

<summary>Custom start Script</summary>

### Custom Start Script

Run this script
```bash
# For Linux with a we server or reverse proxy (like Apache, Nginz, Caddy, Cloudflare Tunnel and else) already in place:
sudo docker run \
--init \
--sig-proxy=false \
--name nextcloud-aio-mastercontainer \
--restart unless-stopped \
--publish 8080:8080 \
--env APACHE_PORT=11000 \
--env APACHE_IP_BINDING=192.168.1.101 \
--env SKIP_DOMAIN_VALIDATION=true
--volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config \
--volume /var/run/docker.sock:/var/run/docker.sock:ro \
nextcloud/all-in-one:latest
```

</details>
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

1. Run this script (Not Recommended)
```bash
# For Linux with a we server or reverse proxy (like Apache, Nginz, Caddy, Cloudflare Tunnel and else) already in place:
sudo docker run \
--init \
--sig-proxy=false \
--name nextcloud-aio-mastercontainer \
--restart unless-stopped \
--publish 8080:8080 \
--env APACHE_PORT=11005 \
--env APACHE_IP_BINDING=192.168.1.101 \
--env SKIP_DOMAIN_VALIDATION=true \
--volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config \
--volume /var/run/docker.sock:/var/run/docker.sock:ro \
nextcloud/all-in-one:latest
```

2. The Recommended way

Run this script.
> [!CAUTION]
> THIS TURNS OFF DOMAIN VALIDATION!! IF YOU DO NOT SET THIS UP PROPERLY YOU WILL NOT HAVE ACCESS AND THIS WILL NOT WORK

```bash
sudo docker run \
--sig-proxy=false \
--name nextcloud-aio-mastercontainer \
--restart always \
--publish 80:80 \
--publish 8080:8080 \
--publish 8443:8443 \
--volume nextcloud_aio_mastercontainer:/mnt/docker-aio-config \
--volume /var/run/docker.sock:/var/run/docker.sock:ro \
-e SKIP_DOMAIN_VALIDATION=true \
nextcloud/all-in-one:latest
```

</details>

### How to properly reset the instance?
If something goes unexpected routes during the initial installation, you might want to reset the AIO installation to be able to start from scratch.

**Please note**: if you already have it running and have data on your instance, you should not follow these instructions as it will delete all data that is coupled to your AIO instance.

Here is how to reset the AIO instance properly:
1. Stop all containers if they are running from the AIO interface
1. Stop the mastercontainer with `sudo docker stop nextcloud-aio-mastercontainer`
1. If the domaincheck container is still running, stop it with `sudo docker stop nextcloud-aio-domaincheck`
1. Check that no AIO containers are running anymore by running `sudo docker ps --format {{.Names}}`. If no `nextcloud-aio` containers are listed, you can proceed with the steps below. If there should be some, you will need to stop them with `sudo docker stop <container_name>` until no one is listed anymore.
1. Check which containers are stopped: `sudo docker ps --filter "status=exited"`
1. Now remove all these stopped containers with `sudo docker container prune`
1. Delete the docker network with `sudo docker network rm nextcloud-aio`
1. Check which volumes are dangling with `sudo docker volume ls --filter "dangling=true"`
1. Now remove all these dangling volumes: `sudo docker volume prune --filter all=1` (on Windows you might need to remove some volumes afterwards manually with `docker volume rm nextcloud_aio_backupdir`, `docker volume rm nextcloud_aio_nextcloud_datadir`). 
1. If you've configured `NEXTCLOUD_DATADIR` to a path on your host instead of the default volume, you need to clean that up as well. (E.g. by simply deleting the directory).
1. Make sure that no volumes are remaining with `sudo docker volume ls --format {{.Name}}`. If no `nextcloud-aio` volumes are listed, you can proceed with the steps below. If there should be some, you will need to stop them with `sudo docker volume rm <volume_name>` until no one is listed anymore.
1. Optional: You can remove all docker images with `sudo docker image prune -a`.
1. And you are done! Now feel free to start over with the recommended docker run command!
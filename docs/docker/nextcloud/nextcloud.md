# Nextcloud

### Install

There are two ways of installing nextcloud using docker and docker compose. Below are the links to both of the ways for installing

[Docker](docs/docker/nextcloud/docs/docker.md)
[Docker Compose](docs/nextcloud/docs/docker-compose.md)



### How to properly reset the instance?
If something goes unexpected routes during the initial installation, you might want to reset the AIO installation to be able to start from scratch.

**Please note**: if you already have it running and have data on your instance, you should not follow these instructions as it will delete all data that is coupled to your AIO instance.

Here is how to reset the AIO instance properly:
1. Stop all containers if they are running from the AIO interface
2. Stop the mastercontainer with 
```bash
sudo docker stop nextcloud-aio-mastercontainer
```
3. If the domaincheck container is still running, stop it with 
```bash
sudo docker stop nextcloud-aio-domaincheck
```
4. Check that no AIO containers are running anymore by running 
```bash
sudo docker ps --format {{.Names}}
```
. If no `nextcloud-aio` containers are listed, you can proceed with the steps below. If there should be some, you will need to stop them with `sudo docker stop <container_name>` until no one is listed anymore.
5. Check which containers are stopped: 
```bash
sudo docker ps --filter "status=exited"
```
6. Now remove all these stopped containers with 
```bash
sudo docker container prune
```
7. Delete the docker network with 
```bash
sudo docker network rm nextcloud-aio
```
8. Check which volumes are dangling with 
```bash
sudo docker volume ls --filter "dangling=true"
```
9. Now remove all these dangling volumes: 
```bash
sudo docker volume prune --filter all=1
```
 (on Windows you might need to remove some volumes afterwards manually with `docker volume rm nextcloud_aio_backupdir`, `docker volume rm nextcloud_aio_nextcloud_datadir`). 
10. If you've configured 
```bash
NEXTCLOUD_DATADIR
```
 to a path on your host instead of the default volume, you need to clean that up as well. (E.g. by simply deleting the directory).
11. Make sure that no volumes are remaining with 
```bash
sudo docker volume ls --format {{.Name}}
```
If no `nextcloud-aio` volumes are listed, you can proceed with the steps below. If there should be some, you will need to stop them with `sudo docker volume rm <volume_name>` until no one is listed anymore.
12. Optional: You can remove all docker images with 
```bash
sudo docker image prune -a
```
13. And you are done! Now feel free to start over with the recommended docker run command!
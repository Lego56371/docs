# Portainer

### Install

To install Portainer you need to run the following commands
```bash
docker volume create portainer_data
```

Then all we need to do is start the container
```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.21.2
```
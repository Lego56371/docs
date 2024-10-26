# Nextcloud behind a cloudflare tunnel

### FIREWALL

It may be necessary to enable ports on the device 8080 and 11000
```bash
sudo ufw allow 8080
sudo ufw allow 11000
sudo ufw reload
```

### NEXTCLOUD AIO

Create a directory and in it the docker-compose.yml file
```bash
mkdir nextcloud-aio && cd nextcloud-aio && nano docker-compose.yml
```

insert code

```yml
version: "3.8"

services:
  nextcloud:
    image: nextcloud/all-in-one:latest
    restart: always
    container_name: nextcloud-aio-mastercontainer 
    volumes:
      - nextcloud_aio_mastercontainer:/mnt/docker-aio-config 
      - /var/run/docker.sock:/var/run/docker.sock:ro 
    ports:
      - 80:80 
      - 8080:8080
    environment: 
      - APACHE_PORT=11000 
      - APACHE_IP_BINDING=0.0.0.0
      - SKIP_DOMAIN_VALIDATION=true

volumes:
  nextcloud_aio_mastercontainer:
    name: nextcloud_aio_mastercontainer
```

Next start the container

```bash
sudo docker compose up -d
```
# Uptime Kuma

### Install

To install Uptime Kuma we need to do the following.

1. Make sure docker and docker compose are installed

2. We need to create a directory for Uptime Kuma. To do that we run these commands
```bash
mkdir kuma && cd kuma
```

3. Now we need to create a docker-compose.yml. To do that we run this command
```bash
touch docker-compose.yml
```

4. Now we need to edit that file
```bash
nano docker-compose up -d
```

And paste the docker-compose contents into that file
```yml
# Simple docker-compose.yml
# You can change your port or volume location

version: '3.3'

services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - ./uptime-kuma-data:/app/data
    ports:
      - 3001:3001  # <Host Port>:<Container Port>
    # Changed this to unless-stopped
    restart: unless-stopped
```

5. Now all we need to do is start the docker container.
```bash
sudo docker compose up -d
```
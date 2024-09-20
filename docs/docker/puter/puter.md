# Puter

### Install

1. We need to create a directory for our docker container
```bash
mkdir puter && cd puter
```

2. Now we need to create a docker-compose.yml
```bash
touch docker-compose.yml
```

3. Now we need to edit the docker-compose.yml
```bash
nano docker-compose.yml
```

4. Now we need to add the contents to the docker-compose.yml
```bash
---
version: "3.8"
services:
  puter:
    container_name: puter
    image: ghcr.io/heyputer/puter:latest
    pull_policy: always
    # build: ./
    restart: unless-stopped
    ports:
      - '4100:4100'
    environment:
      # TZ: Europe/Paris
      # CONFIG_PATH: /etc/puter
      PUID: 1000
      PGID: 1000
    volumes:
      - ./puter/config:/etc/puter
      - ./puter/data:/var/puter
    healthcheck:
      test: wget --no-verbose --tries=1 --spider http://puter.localhost:4100/test || exit 1
      interval: 30s
      timeout: 3s
      retries: 3
      start_period: 30s
```

5. Now all we need to do is start the docker container
```bash
sudo docker compose up -d
```
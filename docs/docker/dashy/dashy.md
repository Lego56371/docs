# Dashy

### Install

To install dashy we can use either docker or docker compose. You can find the docs for both below

#### Docker

To install Dashy using docker we can run the script below
```bash
sudo docker run -d \
  -p 8080:8080 \
  -v ~/my-conf.yml:/app/user-data/conf.yml \
  --name my-dashboard \
  --restart=always \
  lissy93/dashy:latest
```
Then all we have to do is http://ip-address:8080

#### Docker Compose

To install Dashy using docker compose we will follow these steps

1. We need to create a directory and then cd into that directory
```bash
mkdir dashy && cd dashy
```

2. Now we need to create our docker-compose.yml and then copy and paste the contents into that file
```bash
touch docker-compose.yml && nano docker-compose.yml
```

```yml
---
version: "3.8"
services:
  dashy:
    # To build from source, replace 'image: lissy93/dashy' with 'build: .'
    # build: .
    image: lissy93/dashy
    container_name: Dashy
    # Pass in your config file below, by specifying the path on your host machine
    # volumes:
      # - /root/my-config.yml:/app/user-data/conf.yml
    ports:
      - 8080:8080
    # Set any environmental variables
    environment:
      - NODE_ENV=production
    # Specify your user ID and group ID. You can find this by running `id -u` and `id -g`
    #  - UID=1000
    #  - GID=1000
    # Specify restart policy
    restart: unless-stopped
    # Configure healthchecks
    healthcheck:
      test: ['CMD', 'node', '/app/services/healthcheck']
      interval: 1m30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

3. Now all we need to do is start our docker container
```bash
sudo docker compose up -d
```
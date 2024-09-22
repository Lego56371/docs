# Homarr

### Install

To install Homarr we are going to use docker compose. To install Homarr using docker compose follow the steps bellow

1. First we need to create a directory and then cd into it
```bash
mkdir homarr && cd homarr
```

2. Next we need to create the docker-compose.yml and then copy and paste the contents into the file
```bash
touch docker-compose.yml && nano docker-compose.yml
```

And copy the following contents over to that file
```yml
#---------------------------------------------------------------------#
#     Homarr - A simple, yet powerful dashboard for your server.      #
#---------------------------------------------------------------------#
services:
  homarr:
    container_name: homarr
    image: ghcr.io/ajnart/homarr:latest
    # made sure this is unless-stopped and not always
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # Optional, only if you want docker integration
      - ./homarr/configs:/app/data/configs
      - ./homarr/icons:/app/public/icons
      - ./homarr/data:/data
    ports:
      - '7575:7575'
```

3. Next all we need to do is start the docker container. To do that we will run the script below
```bash
sudo docker compose up -d
```
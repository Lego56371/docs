# Homer

### Install

To install Homer we need to run the following commands

1. We need to create the directory and cd into it
```bash
mkdir homer && cd homer
```

2. Next we need to create a docker-compose.yml and the edit it
```bash
touch docker-compose.yml && nano docker-compose.yml
```

3. Next we need to copy the following into the docker-compose.yml
```yml
version: '3.9'
services:
    nginx:
        image: nginx
        logging:
            options:
                max-size: 1g
        restart: always
        volumes:
            - '/var/run/docker.sock:/tmp/docker.sock:ro'
        ports:
            - '80:80'
```

4. Then all we need to do is start the docker container with the following command
```bash
sudo docker compose up -d
```
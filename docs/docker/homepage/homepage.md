# Homepage

### Install

1. First we need to create a directory and then cd into that directory
```bash
mkdir homepage && cd homepage
```

2. Then we need to create a docker-compose.yml
```bash
touch docker-compose.yml
```

3. Now we need to edit the docker-compose.yml and add the contents
```bash
nano docker-compose.yml
```
Then copy and paste the code below into that file
```yml
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    ports:
      - 3000:3000
    volumes:
      - /path/to/config:/app/config # Make sure your local config directory exists
      - /var/run/docker.sock:/var/run/docker.sock # (optional) For docker integrations
```

4. Now all we need to do is start the docker container
```bash
sudo docker compose up
```
Or use the command below to run it in detached mode. RECOMMENDED
```bash
sudo docker compose up -d
```
# NGINX Proxy Manager

### Install

To install NGING Proxy Manager we want to create a directory called nginx
```bash
mkdir nginx && cd nginx
```

Then we want to create a docker-compose.yml
```bash
touch docker-compose.yml
```
Then we want to edit the docker-compose.yml
```bash
nano docker-compose.yml
```

We now want to add the contents of the docker-compose.yml
```yml
version: '3.8'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP

    # Uncomment the next line if you uncomment anything in the section
    # environment:
      # Uncomment this if you want to change the location of
      # the SQLite DB file within the container
      # DB_SQLITE_FILE: "/data/database.sqlite"

      # Uncomment this if IPv6 is not enabled on your host
      # DISABLE_IPV6: 'true'

    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

After that we want to start the docker container
```bash
sudo docker compose up -d
```

Here is the default username and password
```
Email:    admin@example.com
Password: changeme
```

Cloudflare DNS Token
```
mc_AgKeUhMXtX7oZqbMfcfEe7ibDvKVFNLPDHZ95
```
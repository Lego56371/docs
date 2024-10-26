# Installion of MariaDB

Make sure docker and docker compose are installed

1. Create a folder to put our files in called `mariadb` and then open that folder
```bash
mkdir mariadb && cd mariadb
```

2. Now we want to create and edit a `docker-compose.yml`
```bash
touch docker-compose.yml && nano docker-compose.yml
```

3. Now we want to paste the following into that file
```yml
# Use root/example as user/password credentials
version: '3.1'

services:

  db:
    image: mariadb
    # Changed this to unless-stopped
    restart: unless-stopped
    environment:
      MARIADB_ROOT_PASSWORD: B105

  adminer:
    image: adminer
    # Changed this to unless-stopped
    restart: unless-stopped
    ports:
      - 8080:8080
```

4. Now all we need to do is start the docker container
```bash
sudo docker compose up -d
```
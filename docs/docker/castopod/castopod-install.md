# Castopod Installtion

First we need to create a `docker-compose.yml`
```yaml
version: "3.7"

services:
  castopod:
    image: castopod/castopod:latest
    container_name: "castopod"
    volumes:
      - castopod-media:/var/www/castopod/public/media
    environment:
      MYSQL_DATABASE: castopod
      MYSQL_USER: castopod
      MYSQL_PASSWORD: changeme
      CP_BASEURL: "https://castopod.example.com"
      CP_ANALYTICS_SALT: changeme
      CP_CACHE_HANDLER: redis
      CP_REDIS_HOST: redis
      CP_REDIS_PASSWORD: changeme
    networks:
      - castopod
      - castopod-db
    ports:
      - 8000:8000
    restart: unless-stopped

  mariadb:
    image: mariadb:11.2
    container_name: "castopod-mariadb"
    networks:
      - castopod-db
    volumes:
      - castopod-db:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: changeme
      MYSQL_DATABASE: castopod
      MYSQL_USER: castopod
      MYSQL_PASSWORD: changeme
    restart: unless-stopped

  redis:
    image: redis:7.2-alpine
    container_name: "castopod-redis"
    command: --requirepass changeme
    volumes:
      - castopod-cache:/data
    networks:
      - castopod

volumes:
  castopod-media:
  castopod-db:
  castopod-cache:

networks:
  castopod:
  castopod-db:
```
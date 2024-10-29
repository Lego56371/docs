# Jellyfin Installation Guide

First make sure you have docker and docker compose installed

1. Lets create a folder called jellyfin can open that folder
```bash
mkdir jellyfin && cd jellyfin
```

2. Now lets create all the folders we need
```bash
mkdir config && mkdir cache
```

3. Now let create the `docker-compose.yml`
```bash
nano docker-compose.yml
```

And paste the following in that file
```yml
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    user: uid:gid
    network_mode: 'host'
    volumes:
      - /home/rtech-local/jellyfin/config:/config
      - /home/rtech-local/jellyfin/cache:/cache
      - type: bind
        source: /home/rtech-local/media/media
        target: /media
      - type: bind
        source: /home/rtech-local/media/podcast
        target: /media2
        read_only: true
      # Optional - extra fonts to be used during transcoding with subtitle burn-in
      - type: bind
        source: /path/to/fonts
        target: /usr/local/share/fonts/custom
        read_only: true
    restart: 'unless-stopped'
    # Optional - alternative address used for autodiscovery
    environment:
      - JELLYFIN_PublishedServerUrl=http://example.com
    # Optional - may be necessary for docker healthcheck to pass if running in host network mode
    extra_hosts:
      - 'host.docker.internal:host-gateway'
```
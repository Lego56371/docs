# JellyFin

### Install

To install JellyFin we need to run these commands

```bash
docker pull jellyfin/jellyfin:latest  # or docker pull ghcr.io/jellyfin/jellyfin:latest
```

```bash
mkdir -p /srv/jellyfin/{config,cache}
```

```bash
docker run -d -v /srv/jellyfin/config:/config -v /srv/jellyfin/cache:/cache -v /media:/media --net=host jellyfin/jellyfin:latest
```

## My modifation to the last script

```bash
docker run -d -v /srv/jellyfin/config:/config -v /srv/jellyfin/cache:/cache -v /home/btech-local/media:/media --net=host jellyfin/jellyfin:latest
```
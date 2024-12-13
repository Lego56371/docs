# Listmonk Installation

1. First make sure docker is install
```bash
docker --version
```

2. Now we want to make a directory and clone the `docker-compose.yml` into that directory
```bash
mdkir listmonk && curl -LO https://github.com/knadh/listmonk/raw/master/docker-compose.yml
```

3. Now we want to start the container
```bash
docker compose up -d
```
# Authentik

This is my version of the documentation for Authentik

## Installation

To install Authentik I choose to use the docker compose method. Here are the steps I took to install it

1. First we need to pull the `docker-compose.yml` file to our server. First we need to create a directory and cd into it
```bash
mkdir authentik
```

```bash
cd authentik
```

```baah
wget https://goauthentik.io/docker-compose.yml
```

2. Next we need to run the following commands to generate a password and secret key and write them to your .env file:
```bash
echo "PG_PASS=$(openssl rand -base64 36 | tr -d '\n')" >> .env
echo "AUTHENTIK_SECRET_KEY=$(openssl rand -base64 60 | tr -d '\n')" >> .env
```

3. Now all we need to do is start up the docker container in the backgroud. To do that we run the following command
```bash
sudo docker compose up -d
```
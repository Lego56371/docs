# n8n

### Install

To install n8n we need to run the following script after docker has been installed
```bash
docker volume create n8n_data
```
```bash
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

```bash
docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -v n8n_data:/home/node/.n8n \
 -e N8N_SECURE_COOKIE=false \
 docker.n8n.io/n8nio/n8n
```


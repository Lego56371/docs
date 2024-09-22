# Salt Rim

```bash
$ docker run -d \
    --name salt-rim \
    -e API_URL=http://your-bar-assistant-url \
    -e MEILISEARCH_URL=http://your-meilisearch-url \
    -p 8080:8080 \
    barassistant/salt-rim
```

```bash
$ docker run -d \
    --name salt-rim \
    -e API_URL=https://bar-api.ross-cuttriss-tech.tech/bar \
    -e MEILISEARCH_URL=https://bar-search.ross-cuttriss-tech.tech/search \
    -p 8080:8080 \
    barassistant/salt-rim
```
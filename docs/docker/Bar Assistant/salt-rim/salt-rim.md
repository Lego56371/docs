# Salt Rim

```bash
$ docker run -d \
    --name salt-rim \
    -e API_URL=http://your-bar-assistant-url \
    -e MEILISEARCH_URL=http://your-meilisearch-url \
    -p 8080:8080 \
    barassistant/salt-rim
```
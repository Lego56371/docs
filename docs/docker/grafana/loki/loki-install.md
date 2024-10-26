# Loki Installation Docs

1. Make sure you have docker and docker compose installed

2. Create a folder for the loki files to be in & cd into that folder
```bash
mkdir loki
```

```bash
cd loki
```

3. Create and edit the docker compose file and copy the following contents into that file
```yml
version: "3"
networks:
  loki:
services:
  loki:
    image: grafana/loki:2.4.0
    volumes:
      - /home/rtech-local/docker_volumes/loki:/etc/loki
    ports:
      - "3100:3100"
    restart: unless-stopped
    command: -config.file=/etc/loki/loki-config.yml
    networks:
      - loki
  promtail:
    image: grafana/promtail:2.4.0
    volumes:
      - /var/log:/var/log
      - /home/rtech-local/docker_volumes/promtail:/etc/promtail
    # ports:
    #   - "1514:1514" # this is only needed if you are going to send syslogs
    restart: unless-stopped
    command: -config.file=/etc/promtail/promtail-config.yml
    networks:
      - loki
  grafana:
    image: grafana/grafana:latest
    user: "1000"
    volumes:
    - /home/rtech-local/docker_volumes/grafana:/var/lib/grafana
    ports:
      - "3000:3000"
    restart: unless-stopped
    networks:
      - loki
```


Loki config file

Create a loki config file
```bash
nano loki/loki-config.yml
```

And paste the following in there
```yml
auth_enabled: false

server:
  http_listen_port: 3100
  grpc_listen_port: 9096

common:
  path_prefix: /tmp/loki
  storage:
    filesystem:
      chunks_directory: /tmp/loki/chunks
      rules_directory: /tmp/loki/rules
  replication_factor: 1
  ring:
    instance_addr: 127.0.0.1
    kvstore:
      store: inmemory

schema_config:
  configs:
    - from: 2020-10-24
      store: boltdb-shipper
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 24h

ruler:
  alertmanager_url: http://localhost:9093
```

promtail config
```bash
nano promtail/promtail-config.yml
```


```yml
server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://loki:3100/loki/api/v1/push

scrape_configs:

# local machine logs

- job_name: local
  static_configs:
  - targets:
      - localhost
    labels:
      job: varlogs
      __path__: /var/log/*log
  
## docker logs

#- job_name: docker 
#  pipeline_stages:
#    - docker: {}
#  static_configs:
#    - labels:
#        job: docker
#        __path__: /var/lib/docker/containers/*/*-json.log

# syslog target

#- job_name: syslog
#  syslog:
#    listen_address: 0.0.0.0:1514 # make sure you also expose this port on the container
#    idle_timeout: 60s
#    label_structured_data: yes
#    labels:
#      job: "syslog"
#  relabel_configs:
#    - source_labels: ['__syslog_message_hostname']
#      target_label: 'host'
```
# Grafana

### Install

Complete the following steps to install Grafana from the APT repository:

1. Install the prerequisite packages:
```bash
sudo apt-get install -y apt-transport-https software-properties-common wget
```

2. Import the GPG key:
```bash
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

3. To add a repository for stable releases, run the following command:
```bash
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

4. Run the following command to update the list of available packages:
```bash
# Updates the list of available packages
sudo apt-get update
```

5. To install Grafana OSS, run the following command:
```bash
# Installs the latest OSS release:
sudo apt-get install grafana -y
```

### Start Grafana Server

1. To set Grafana to start on boot run this command
```bash
sudo systemctl enable grafana-server.service
```

echo "DOMAIN=http://10.0.0.44:8080
# Remove 'with_grafana' below if you want to use existing grafana
# Add 'with_prometheus' below to optionally enable a local prometheus for oncall metrics
# e.g. COMPOSE_PROFILES=with_grafana,with_prometheus
COMPOSE_PROFILES=with_prometheus
# to setup an auth token for prometheus exporter metrics:
# PROMETHEUS_EXPORTER_SECRET=my_random_prometheus_secret
# also, make sure to enable the /metrics endpoint:
# FEATURE_PROMETHEUS_EXPORTER_ENABLED=True
SECRET_KEY=ahfjkdshflkjhkdhkasdfaldkfjakdlf > .env


```
Kn5xo-sG6BXKTVvdSjHEdsWCIzCZ2dHJUfbl2vhjDI2oRSjsucM_cBV1FSoEU9vF1Ib0cY-kP-T4Ixa09d2FmA==
```
# Grafana
Grafana is a multi-platform open-source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.

# Why do we need Grafana?
Grafana allows you to query, visualize, alert, and understand your metrics no matter where they are stored.

# What Features Does Grafana Provide?
Visualization
Alerts
Data Unification
Open-Source
Log Exploration
Dashboard Display

# Install Grafana on Debian or Ubuntu

sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

# Stable release
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

# Update the list of available packages
sudo apt-get update

# Install the latest OSS release:
sudo apt-get install grafana
# To start Grafana Server
sudo /bin/systemctl status grafana-server

# What is Loki?
Loki is a log aggregation system designed to store and query logs from all your applications and infrastructure. Loki Acts as data store for Grafana

Install Loki and Promtail using Docker

# Download Loki Config
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml

# What is Promtail?

Promtail is the agent, responsible for gathering logs and sending them to Loki. loki is the main server, responsible for storing logs and processing queries. Grafana for querying and displaying the logs.

# Run Loki Docker container
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml

# Download Promtail Config
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml

# Run Promtail Docker container
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml





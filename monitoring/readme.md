## Prerequisite

- Using **RHEL** Linux
- Download **Docker**

## Node exporter download and setup

```bash
# Download the prometheus node exporter
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz

# Unzip the folder
tar -xvf node_exporter-1.9.1.linux-amd64.tar.gz

# Copy and paste the node_exporter to /usr/bin to access the command globally
cp node_exporter-1.9.1.linux-amd64/node_exporter /usr/bin/node_exporter
```

### Create node exporter as systemd service

```bash
# Create the file in this location
vim /etc/systemd/system/node_exporter.service
```

```bash
# Copy the content and paste in the file
[Unit]
Description=Node Exporter service
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
Restart=always
RestartSec=1
User=root
ExecStart=/usr/bin/node_exporter –collector.systemd –collector.processes

[Install]
WantedBy=multi-user.target
```

```bash
# Start and enable the service
systemctl enable --now node_exporter
```

### Access the node exporter

```bash
# Disable the firewall
systemctl disable --now firewalld
```

```bash
# Change the server-ip
http://<server-ip>:9100
```

## To setup prometheus, alert manager, grafana run this docker compose file

```bash
docker compose up --detach
```

### Access the prometheus

```bash
# Change the server-ip
http://<server-ip>:9090
```

### Access the Alert manager

```bash
# Change the server-ip
http://<server-ip>:9093
```

### Access the grafana

```bash
# Change the server-ip
http://<server-ip>:3000
```

Default username and password is admin

### In grafana add prometheus as data source and the prometheus server url to http://<server-ip>:9090

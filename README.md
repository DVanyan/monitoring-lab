![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)

![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

# Monitoring Lab

Full observability and monitoring lab built with Prometheus, Grafana, Alertmanager, Node Exporter, cAdvisor and Blackbox Exporter using Docker Compose on Ubuntu Server.

## Overview

This project demonstrates a production-like monitoring stack for Linux hosts, Docker containers and HTTP endpoints.

The lab includes:
- Linux host monitoring
- Docker container monitoring
- HTTP/HTTPS uptime monitoring
- Prometheus alerting
- Telegram notifications
- Persistent Grafana storage
- Incident simulation using stress testing

---

# Architecture

![Architecture Dashboard](./screenshots/Architecture.jpg)

---

# Stack

- Ubuntu Server 24.04
- Docker
- Docker Compose
- Prometheus
- Grafana
- Alertmanager
- Node Exporter
- cAdvisor
- Blackbox Exporter
- Telegram Bot API

---

# Features

## Linux Host Monitoring
- CPU usage
- Memory usage
- Disk usage
- Load average
- Network traffic
- Filesystem monitoring

## Docker Container Monitoring
- Container CPU usage
- Container memory usage
- Network traffic
- Container statistics

## Uptime Monitoring
- HTTP/HTTPS probing
- SSL monitoring
- Response time monitoring
- Availability checks

## Alerting
- High CPU alerts
- Low memory alerts
- Telegram notifications
- Alertmanager routing

---

# Dashboards

## Node Exporter Dashboard

![Node Exporter Dashboard](./screenshots/Node_Exporter.jpg)

---

## cAdvisor Dashboard

![cAdvisor](./screenshots/Cadvisor.jpg)

---

## Blackbox Exporter Dashboard

![Blackbox Dashboard](./screenshots/Blackbox.jpg)

---

## Prometheus Dashboard

![Prometheus Dashboard](./screenshots/Prometheus.jpg)

---

## Alertmanager Dashboard

![Prometheus_Alert Dashboard](./screenshots/Prometheus_Alert.jpg)

---

# Prometheus Alerts

## High CPU Usage Alert

```yaml
- alert: HighCPUUsage
  expr: 100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[2m])) * 100) > 80
  for: 1m
```

---

# Telegram Notifications

The monitoring stack sends real-time Telegram notifications through Alertmanager.

Example workflow:

High CPU Usage         
     ↓ 
Prometheus Alert        
     ↓ 
Alertmanager         
     ↓ 
Telegram Notification 

![Telegram Notification](./screenshots/Telegram.jpg)

---

# How to Run

## Clone repository

```bash
git clone https://github.com/DVanyan/monitoring-lab.git
cd monitoring-lab
``` 

## Prepare Grafana persistent storage

Grafana stores runtime data in `/var/lib/grafana`.  
This directory is mounted from `./grafana/data` on the host.

Create the directory and set correct permissions:

```bash
mkdir -p grafana/data
sudo chown -R 472:472 grafana/data
sudo chmod -R 775 grafana/data
```

## Start monitoring stack

```bash
docker compose up -d
```

## Open services

Grafana:
http://SERVER_IP:3000 

Prometheus:
http://SERVER_IP:9090 

Alertmanager:
http://SERVER_IP:9093 

---

# Grafana Dashboards

Imported dashboards:
- 1860 — Node Exporter Full
- 14282 — cAdvisor Exporter
- 7587 — Blackbox Exporter
- 19105 — Prometheus Monitoring

---

# Incident Simulation

CPU stress testing was used to simulate production incidents:

sudo apt install -y stress

bash stress --cpu 4 

This triggers:
- Prometheus alerts
- Alertmanager notifications
- Telegram alerts

---

# Skills Demonstrated

- Linux Administration
- Docker & Docker Compose
- Monitoring & Observability
- Prometheus & PromQL
- Grafana Dashboards
- Alerting Systems
- Infrastructure Troubleshooting
- Container Monitoring
- Uptime Monitoring

---

# Future Improvements

- Loki log aggregation
- Promtail integration
- Kubernetes monitoring
- Helm deployment
- SSL expiration alerts
- Custom Grafana dashboards
- CI/CD integration

---

# Author

David Vanyan

LFCS Certified Linux Administrator

[![LFCS](https://images.credly.com/size/220x220/images/1e6611ca-8afe-4ecc-ad4d-305fba52ee7e/1_LFCS-600x600.png)](https://www.credly.com/badges/eb28bbcb-1a81-4e01-98bf-b6d1e6c674be/public_url)

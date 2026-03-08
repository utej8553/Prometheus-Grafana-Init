# Prometheus & Grafana Setup

### Prometheus

Access Prometheus UI:

```
http://localhost:9090
```

### Grafana

Access Grafana UI:

```
http://localhost:3000
```

Default credentials:

```
username: admin
password: admin
```

---

# Docker Compose Configuration

Prometheus and Grafana are started using the following **docker-compose.yml**.

```yaml
version: "3"

services:

  prometheus:
    image: prom/prometheus
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"
```

Prometheus loads its configuration from the mounted **prometheus.yml** file.

---

# Running the Monitoring Stack

Start the services using:

```
docker compose up -d
```

Check running containers:

```
docker ps
```

---

# Accessing the Services

Prometheus:

```
http://localhost:9090
```

Grafana:

```
http://localhost:3000
```

---

# Connecting Grafana to Prometheus

To visualize metrics in Grafana:

Set the Prometheus URL:

```
http://prometheus:9090
```

Click **Save & Test** to verify the connection.

---

# Spring Boot Configuration for Metrics


```
management.endpoints.web.exposure.include=*
management.endpoint.prometheus.enabled=true
management.metrics.export.prometheus.enabled=true
```

These configurations enable the **Prometheus metrics endpoint**.

The metrics will be available at:

```
/actuator/prometheus
```

Example endpoint:

```
http://localhost:8080/actuator/prometheus
```

Prometheus scrapes this endpoint periodically to collect application metrics.

---


Prometheus scrapes metrics from the application endpoint and Grafana displays them through dashboards.

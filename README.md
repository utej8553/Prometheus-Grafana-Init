# Prometheus & Grafana Setup

### Prometheus

Default access URL:

```
http://localhost:9090
```

### Grafana

Grafana is a visualization tool that connects to Prometheus and displays metrics in the form of dashboards.

Default access URL:

```
http://localhost:3000
```

Default login credentials:

```
username: admin
password: admin
```

## Docker Compose Configuration

The services are started using the following `docker-compose.yml`.

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

Prometheus loads its configuration from the `prometheus.yml` file mounted into the container.

## Running the Stack

Start the services using:

```
docker compose up -d
```

This will launch both containers in the background.

Verify running containers:

```
docker ps
```

## Accessing the Services

Prometheus UI:

```
http://localhost:9090
```

Grafana UI:

```
http://localhost:3000
```

## Connecting Grafana to Prometheus

To visualize metrics in Grafana:

1. Open Grafana in the browser.
2. Navigate to **Connections → Data Sources**.
3. Click **Add data source**.
4. Select **Prometheus**.

Set the Prometheus URL:

```
http://prometheus:9090
```

Click **Save & Test**.

Grafana will now be connected to Prometheus and ready to create or import dashboards.

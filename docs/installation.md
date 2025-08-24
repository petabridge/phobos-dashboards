# Installation Guide

## Prerequisites

Before installing the Phobos dashboards, ensure you have:

1. **Grafana** (v9.0 or higher recommended)
2. **Prometheus** configured as a data source in Grafana
3. **Phobos 2.x** with OpenTelemetry metrics enabled
4. **OpenTelemetry Collector** configured to export metrics to Prometheus

## Quick Start

### 1. Configure Phobos for OpenTelemetry

Ensure your Phobos configuration includes OpenTelemetry exporters:

```hocon
phobos {
  monitoring {
    provider = "OpenTelemetry"
    opentelemetry {
      exporter = "otlp"
      endpoint = "http://localhost:4317"
    }
  }
}
```

### 2. Configure OpenTelemetry Collector

Example configuration for the OpenTelemetry Collector:

```yaml
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: 0.0.0.0:4317

exporters:
  prometheus:
    endpoint: "0.0.0.0:8889"

service:
  pipelines:
    metrics:
      receivers: [otlp]
      exporters: [prometheus]
```

### 3. Configure Prometheus

Add the OpenTelemetry Collector as a scrape target in your Prometheus configuration:

```yaml
scrape_configs:
  - job_name: 'otel-collector'
    scrape_interval: 10s
    static_configs:
      - targets: ['localhost:8889']
```

### 4. Import Dashboards into Grafana

1. Open Grafana and navigate to **Dashboards** → **Import**
2. Upload the dashboard JSON file or paste its contents
3. Select your Prometheus data source
4. Click **Import**

## Available Dashboards

### Cluster Overview Dashboard
**File**: `dashboards/cluster-overview.json`

This dashboard provides:
- Actor system health metrics
- Message processing rates
- Actor lifecycle events
- Cluster membership status
- Resource utilization

### Cluster Latencies Dashboard
**File**: `dashboards/cluster-latencies.json`

This dashboard focuses on:
- Message processing latencies
- Percentile distributions (p50, p90, p95, p99)
- Latency trends over time
- Slow message identification

## Configuration Options

### Dashboard Variables

Both dashboards include configurable variables:

- **`cluster`**: Filter by Akka.NET cluster name
- **`system`**: Filter by actor system name
- **`node`**: Filter by specific cluster node
- **`interval`**: Time aggregation interval

### Customizing Metrics

To modify metric queries or add custom panels:

1. Edit the dashboard in Grafana
2. Update the Prometheus queries as needed
3. Export the modified dashboard JSON
4. Submit a PR with your improvements

## Troubleshooting

### No Data Appearing

1. Verify Phobos is configured with OpenTelemetry provider
2. Check OpenTelemetry Collector is running and receiving metrics
3. Confirm Prometheus is scraping the collector endpoint
4. Verify the Prometheus data source in Grafana

### Missing Metrics

Ensure your Phobos configuration includes all required metric categories:

```hocon
phobos {
  monitoring {
    metrics {
      actors = on
      cluster = on
      persistence = on
      dispatchers = on
    }
  }
}
```

### Performance Issues

For large clusters, consider:
- Adjusting the scrape interval in Prometheus
- Increasing dashboard refresh rates
- Using recording rules for frequently-queried metrics

## Support

For additional help:
- [Phobos Documentation](https://phobos.petabridge.com/)
- [GitHub Issues](https://github.com/petabridge/phobos-dashboards/issues)
- [Petabridge Support](https://petabridge.com/contact)
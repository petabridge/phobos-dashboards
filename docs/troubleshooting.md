# Troubleshooting Guide

## Common Issues and Solutions

### Dashboard Shows "No Data"

#### 1. Verify Phobos Configuration

Ensure Phobos is configured to use OpenTelemetry:

```hocon
phobos {
  monitoring {
    provider = "OpenTelemetry"
    opentelemetry {
      exporter = "otlp"
      endpoint = "http://localhost:4317"
      protocol = "grpc"
    }
  }
}
```

#### 2. Check OpenTelemetry Collector Status

```bash
# Check if collector is running
curl http://localhost:13133/

# Check metrics endpoint
curl http://localhost:8889/metrics
```

#### 3. Verify Prometheus Configuration

Test Prometheus targets:
1. Navigate to Prometheus UI (typically http://localhost:9090)
2. Go to Status → Targets
3. Verify "otel-collector" target is UP

#### 4. Test Metric Availability

Query Prometheus directly:
```promql
# Check for any Akka metrics
{__name__=~"akka.*"}

# Check for specific metric
akka_actor_created_total
```

### Incorrect or Missing Labels

#### Issue: Cluster name not appearing

**Solution**: Ensure resource attributes are set in Phobos:

```hocon
phobos {
  monitoring {
    opentelemetry {
      resource-attributes {
        "service.name" = "my-service"
        "cluster.name" = "my-cluster"
        "deployment.environment" = "production"
      }
    }
  }
}
```

### High Memory Usage in Grafana

#### Issue: Dashboard queries consuming too much memory

**Solutions**:

1. **Reduce time range**: Use shorter time windows for queries
2. **Add recording rules** in Prometheus for complex queries:

```yaml
groups:
  - name: phobos_aggregations
    interval: 30s
    rules:
      - record: akka:message_rate_5m
        expr: rate(akka_actor_messages_received_total[5m])
```

3. **Increase query limits** in Grafana data source settings

### Latency Metrics Not Showing

#### Issue: Histogram metrics not displaying percentiles

**Solution**: Ensure buckets are properly configured:

```promql
# Correct query for percentiles
histogram_quantile(0.95,
  sum(rate(akka_actor_message_processing_time_seconds_bucket[5m])) 
  by (le, actor_class)
)
```

### Dashboard Import Fails

#### Issue: "Invalid JSON" error when importing

**Solutions**:

1. Validate JSON syntax:
```bash
# Using jq
jq . dashboard.json

# Using Python
python -m json.tool dashboard.json
```

2. Check for version compatibility:
   - Grafana version should be 9.0+
   - Dashboard schema version compatibility

### Metrics Have High Cardinality

#### Issue: Too many unique metric series

**Solutions**:

1. **Limit actor path depth** in Phobos configuration:

```hocon
phobos {
  monitoring {
    actor-path-depth = 3  # Limit path depth to reduce cardinality
  }
}
```

2. **Use metric relabeling** in Prometheus:

```yaml
metric_relabel_configs:
  - source_labels: [actor_path]
    regex: '.*/(user|system)/.*'
    target_label: actor_category
```

### Clock Skew Issues

#### Issue: Metrics appear in the future or past

**Solution**: Ensure time synchronization:

```bash
# Check system time
timedatectl status

# Sync with NTP
sudo ntpdate -s time.nist.gov
```

### Performance Issues

#### Slow Dashboard Loading

1. **Optimize queries**:
   - Use `by` clauses to limit aggregation
   - Add time constraints: `[5m]` instead of unbounded
   - Use `increase()` instead of `rate()` for counters when appropriate

2. **Enable caching**:
   - Configure Prometheus query caching
   - Enable Grafana dashboard caching

3. **Reduce refresh rate**:
   - Change dashboard auto-refresh from 5s to 30s or 1m

#### Missing Recent Data

Check for lag in the pipeline:

```bash
# Check collector metrics for dropped data
curl http://localhost:8888/metrics | grep dropped

# Check Prometheus scrape duration
histogram_quantile(0.99, prometheus_target_scrape_duration_seconds)
```

## Debugging Commands

### Check Component Versions

```bash
# Grafana version
curl -s http://localhost:3000/api/health | jq .version

# Prometheus version
curl -s http://localhost:9090/api/v1/status/buildinfo | jq .data.version

# OpenTelemetry Collector version
otelcol --version
```

### Verify Metric Flow

1. **At Phobos**: Enable debug logging
```hocon
akka.loglevel = DEBUG
phobos.monitoring.log-level = DEBUG
```

2. **At Collector**: Check debug endpoints
```bash
curl http://localhost:55679/debug/tracez
curl http://localhost:55679/debug/pipelinez
```

3. **At Prometheus**: Check scrape errors
```promql
up{job="otel-collector"}
prometheus_target_scrape_sample_limit
```

## Getting Help

If issues persist:

1. **Collect diagnostic information**:
   - Phobos configuration
   - OpenTelemetry Collector configuration
   - Prometheus configuration
   - Grafana dashboard JSON
   - Sample of metrics from Prometheus

2. **Check logs** from all components:
   - Application logs (Phobos)
   - OpenTelemetry Collector logs
   - Prometheus logs
   - Grafana logs

3. **Contact support**:
   - [GitHub Issues](https://github.com/petabridge/phobos-dashboards/issues)
   - [Petabridge Support](https://petabridge.com/contact)
   - [Akka.NET Discord](https://discord.gg/GSCfPwhbWP)
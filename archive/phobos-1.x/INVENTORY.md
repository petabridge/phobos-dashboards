# Phobos 1.x Dashboard Archive Inventory

This archive contains all Phobos 1.x dashboards that were deprecated in favor of Phobos 2.x OpenTelemetry-based dashboards.

## Archive Contents

### AppInsights Dashboards
- **phobos-appinsights-ARM-template.json** - Azure Resource Manager template for Phobos metrics in Application Insights
- **phobos-appinsights-single-system-ARM-template.json** - ARM template for single-system Phobos deployments
- **phobos-appinsights-single-system-template.workbook** - Azure Workbook template for single-system monitoring
- **phobos-appinsights-template.workbook** - General Azure Workbook template for Phobos metrics

### DataDog Dashboards

#### DataDog Client Integration
- **phobos-akka.net-cluster-metrics-datadog.json** - Cluster-wide metrics dashboard using DataDog client
- **phobos-akka.net-metrics-datadog.json** - Individual actor system metrics using DataDog client

#### DogStatsD Integration
- **phobos-akka.net-cluster-metrics-dogstatsd.json** - Cluster-wide metrics dashboard using DogStatsD
- **phobos-akka.net-metrics-dogstatsd.json** - Individual actor system metrics using DogStatsD

### InfluxDB Dashboard
- **phobos-akkanet-cluster-overview-influxdb.json** - Grafana dashboard for InfluxDB data source

### Prometheus Dashboard
- **phobos-akkanet-cluster-overview.json** - Original Prometheus-based Grafana dashboard for Phobos 1.x

## Migration Guide

These dashboards are compatible with Phobos 1.x metrics format. For Phobos 2.x deployments, please use the new OpenTelemetry-based dashboards available in the main repository.

### Key Differences in Phobos 2.x
- OpenTelemetry-based metric collection
- Updated metric names following OTEL conventions
- Enhanced latency tracking and percentile calculations
- Improved resource labeling and attribution

## Support

These dashboards are archived and no longer actively maintained. For current deployments, please migrate to Phobos 2.x and use the updated dashboards.

For migration assistance, please refer to the [Phobos documentation](https://phobos.petabridge.com/) or contact [Petabridge support](https://petabridge.com/contact).
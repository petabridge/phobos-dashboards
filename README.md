# Phobos Dashboards 📊

Production-ready [Grafana dashboards](https://grafana.com/) for monitoring [Akka.NET](https://getakka.net/) applications instrumented with [Phobos](https://phobos.petabridge.com/) - the observability engine for Akka.NET.

## Overview 🎯

These dashboards provide comprehensive monitoring capabilities for Akka.NET applications using Phobos's OpenTelemetry metrics export. Monitor cluster health, actor performance, message processing latencies, and system resource utilization in real-time.

## Prerequisites ✅

- Grafana 8.0+
- Prometheus data source configured
- Akka.NET application instrumented with [Phobos 2.x](https://phobos.petabridge.com/articles/setup/index.html)
- OpenTelemetry metrics exporter configured

## Available Dashboards 📈

### Cluster Overview Dashboard 🌐

Monitor your entire Akka.NET cluster's health and performance metrics at a glance.

#### Cluster Status and Node Health
![Cluster Status](images/cluster-overview-top.png)
*Real-time cluster membership tracking with node status, message rates, and instance details*

#### Logging, and Error Tracking
![Logging and Actor Metrics](images/cluster-overview-middle.png)
*Monitor logging activity and exception tracking*

#### Actor Counts, Message Throughputs, and Backpressure Monitoring

![Akka.NET Actor Counts, Message Throughputs, and Backpressure Monitoring](images/cluster-actor-metrics.png)
*Track actor message processing, backlog, and volumes. Record actor populations per-node, per-application.*

#### Sharding Statistics and Message Flow
![Sharding Statistics](images/cluster-overview-bottom.png)
*Detailed sharding distribution across nodes with message type breakdowns and throughput analysis*

**Key Features:**
- Real-time cluster membership status with Up/Down/Joining/Leaving states
- Node health and availability monitoring with per-instance metrics
- Message throughput and processing rates by message type
- Actor system metrics across all nodes including mailbox backlogs
- Exception tracking with detailed type breakdown
- Sharding statistics for distributed actors

**Use Cases:**
- Production cluster monitoring and health checks
- Capacity planning and scaling decisions
- Incident detection and response
- Performance baseline establishment
- Sharding distribution analysis

### Actor Performance Dashboard ⚡

Deep-dive into individual actor performance metrics and message processing patterns.

#### Actor Overview and Key Metrics
![Actor Overview](images/actor-performance-top.png)
*Real-time actor counts, message volumes, throughput rates, and latency heatmaps*

#### Detailed Performance Analysis
![Performance Analysis](images/actor-performance-bottom.png)
*Message processing latencies, mailbox depths, and per-instance throughput metrics*

**Key Features:**
- Live actor count monitoring across the cluster
- Message processing latency percentiles (P50, P95, P99)
- Latency heatmap visualization for pattern detection
- Per-actor mailbox depth tracking (backlog monitoring)
- Message type distribution and breakdown
- Individual actor throughput metrics by type
- Per-instance performance comparison
- Actor lifecycle events (starts, stops, restarts)

**Use Cases:**
- Performance bottleneck identification
- Actor optimization and tuning
- Message flow analysis and patterns
- Debugging actor-specific issues
- Capacity planning for actor systems
- Latency spike investigation

## Installation 🚀

**[→ Import Cluster Overview Dashboard from Grafana Cloud](https://grafana.com/grafana/dashboards/15637-akka-net-cluster-phobos-2-5-metrics/)**

**[→ Import Actor Performance Dashboard from Grafana Cloud](https://grafana.com/grafana/dashboards/15638-akka-net-cluster-phobos-2-x-message-latency-metrics-prometheus-data-source/)**

Or import manually:

1. Navigate to **Dashboards** → **Import** in Grafana
2. Copy the JSON content from the dashboard files in this repo
3. Paste into the import dialog
4. Select your Prometheus data source

## Configuration ⚙️

**[→ Phobos Setup Guide](https://phobos.petabridge.com/articles/setup/index.html)**

### Dashboard Variables

Both dashboards support the following template variables:

- **`$cluster`** - Filter by Akka.NET cluster name
- **`$node`** - Filter by specific node/host
- **`$actor_system`** - Filter by actor system name
- **`$actor_path`** - Filter by actor path (Actor Performance dashboard)

## Metrics Reference 📊

### Key Metrics Monitored

- **`akka_messages_received_total`** - Total messages received by actors
- **`akka_messages_processed_duration`** - Message processing latency histograms
- **`akka_actor_restarts_total`** - Actor restart counts
- **`akka_cluster_members`** - Current cluster membership
- **`akka_mailbox_size`** - Actor mailbox queue depths
- **`akka_deadletters_total`** - Dead letter counts
- **`akka_system_cpu_usage`** - CPU utilization
- **`akka_system_memory_used`** - Memory consumption

For a complete list of available metrics, see the [Phobos Metrics Documentation](https://phobos.petabridge.com/articles/metrics/index.html).

## Troubleshooting 🔧

### Common Issues

**Dashboard shows "No Data":**
- Verify Prometheus is receiving metrics from your application
- Check the data source configuration in Grafana
- Ensure time range selection includes data points
- Validate metric names match your Phobos version

**Missing Panels or Metrics:**
- Confirm Phobos monitoring features are enabled
- Check OpenTelemetry exporter configuration
- Verify Prometheus scrape configuration
- Review application logs for metric export errors

## Support 💬

- [Phobos Documentation](https://phobos.petabridge.com/)
- [Petabridge Support](https://petabridge.com/support/)
- [Akka.NET Discord](https://discord.gg/GSCfPwhbWP)
- [GitHub Issues](https://github.com/petabridge/phobos-dashboards/issues)

## License 📄

Copyright © 2015-2025 [Petabridge, LLC](https://petabridge.com/)

These dashboards are provided as part of the Phobos product suite. See [Phobos licensing](https://phobos.petabridge.com/articles/licensing.html) for details.
---

Built with ❤️ by [Petabridge](https://petabridge.com/) - Your Akka.NET Success Partner

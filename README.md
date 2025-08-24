# Phobos Dashboards 📊

Production-ready Grafana dashboards for monitoring [Phobos](https://phobos.petabridge.com/) Akka.NET applications with OpenTelemetry.

[![Lint Dashboards](https://github.com/petabridge/phobos-dashboards/actions/workflows/dashboard-lint.yml/badge.svg)](https://github.com/petabridge/phobos-dashboards/actions/workflows/dashboard-lint.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

## 🚀 Quick Start

1. **Configure Phobos 2.x** with OpenTelemetry provider
2. **Set up OpenTelemetry Collector** to export metrics to Prometheus
3. **Import dashboards** into Grafana from the `/dashboards` directory

See [Installation Guide](docs/installation.md) for detailed instructions.

## 📈 Available Dashboards

### Cluster Overview Dashboard
Comprehensive monitoring of your Akka.NET cluster including:
- Actor system health and lifecycle metrics
- Message processing rates and trends
- Cluster membership and node status
- Resource utilization and dispatcher metrics

### Cluster Latencies Dashboard
Deep dive into performance metrics:
- Message processing latency percentiles (p50, p90, p95, p99)
- Latency distribution histograms
- Slow message identification
- Performance trend analysis

## 📚 Documentation

- [Installation Guide](docs/installation.md) - Step-by-step setup instructions
- [Metrics Reference](docs/metrics-reference.md) - Complete list of available metrics
- [Troubleshooting](docs/troubleshooting.md) - Common issues and solutions

## 🔄 Migration from Phobos 1.x

Legacy Phobos 1.x dashboards have been archived and are available in the [releases](https://github.com/petabridge/phobos-dashboards/releases) section. See [RELEASE_NOTES.md](RELEASE_NOTES.md) for migration guidance.

## 🛠️ Requirements

- **Grafana** 9.0+
- **Prometheus** as data source
- **Phobos** 2.x with OpenTelemetry
- **OpenTelemetry Collector** configured for Prometheus export

## 🤝 Contributing

We welcome contributions! Please ensure:
- Dashboards pass linting checks (`dashboard-linter`)
- Documentation is updated for new features
- Screenshots are included for visual changes

## 📦 Other Monitoring Solutions

This repository also includes Phobos 2.x dashboards for:
- **Azure Application Insights** - OpenTelemetry-based workbooks in [`/integrations/appinsights`](integrations/appinsights/)
- **DataDog** - Native DataDog dashboards in [`/integrations/datadog`](integrations/datadog/)

## 📄 License

This project is licensed under the Apache 2.0 License - see the [LICENSE](LICENSE) file for details.

## 💬 Support

- [GitHub Issues](https://github.com/petabridge/phobos-dashboards/issues)
- [Petabridge Support](https://petabridge.com/contact)
- [Akka.NET Discord](https://discord.gg/GSCfPwhbWP)

---

Maintained by [Petabridge](https://petabridge.com/), the Akka.NET experts.
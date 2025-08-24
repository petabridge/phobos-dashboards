# Release Notes

## v2.0.0 - Repository Restructure and Legacy Archive

### Major Changes

#### 🗄️ Legacy Dashboard Archival
- Archived all Phobos 1.x dashboards to preserve historical monitoring capabilities
- Legacy dashboards are now available as a separate release artifact
- Includes comprehensive inventory documentation for archived dashboards

#### 🎯 Focus on Phobos 2.x OpenTelemetry Dashboards
- Repository now exclusively maintains Phobos 2.x OpenTelemetry-based dashboards
- Simplified structure with clear focus on modern observability standards
- Two primary dashboards:
  - **Cluster Overview**: Complete view of Akka.NET cluster health and metrics
  - **Cluster Latencies**: Detailed latency analysis and percentile tracking

#### 🔧 CI/CD Implementation
- Added GitHub Actions workflow for dashboard validation using Grafana's dashboard-linter
- Automated release process for dashboard distribution
- Quality gates ensure dashboard JSON validity and best practices compliance

#### 📚 Enhanced Documentation
- Comprehensive installation guide with prerequisites and configuration
- Detailed metrics reference documenting all available Phobos metrics
- Troubleshooting guide for common issues and solutions
- Migration path from Phobos 1.x to 2.x dashboards

### Breaking Changes

- Removed Phobos 1.x dashboards from main branch (available in archive)
- Changed directory structure - dashboards now in `/dashboards` directory
- Requires Phobos 2.x with OpenTelemetry provider

### Migration Guide

For users upgrading from Phobos 1.x dashboards:

1. Download the legacy archive from the releases page if you need historical dashboards
2. Update Phobos to 2.x with OpenTelemetry configuration
3. Import new dashboards from `/dashboards` directory
4. Refer to `/docs/installation.md` for detailed setup instructions

### Archived Dashboards

The following dashboards have been archived and are available in the v1.0-legacy release:

- **AppInsights**: Phobos 1.x Azure Application Insights dashboards
- **DataDog**: Phobos 1.x DataDog and DogStatsD dashboards
- **InfluxDB**: Legacy InfluxDB Grafana dashboard
- **Prometheus**: Original Phobos 1.x Prometheus dashboard

### Contributors

- Repository restructuring and CI/CD implementation
- Documentation improvements
- Legacy dashboard archival

### Support

For questions or issues:
- [GitHub Issues](https://github.com/petabridge/phobos-dashboards/issues)
- [Petabridge Support](https://petabridge.com/contact)
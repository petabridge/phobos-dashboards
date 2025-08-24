# Phobos Metrics Reference

This document describes the OpenTelemetry metrics exported by Phobos 2.x and displayed in the Grafana dashboards.

## Actor Metrics

### Actor Lifecycle

- **`akka_actor_created_total`**
  - Type: Counter
  - Description: Total number of actors created
  - Labels: `system`, `dispatcher`, `actor_class`, `path`

- **`akka_actor_stopped_total`**
  - Type: Counter
  - Description: Total number of actors stopped
  - Labels: `system`, `dispatcher`, `actor_class`, `path`

- **`akka_actor_restarted_total`**
  - Type: Counter
  - Description: Total number of actor restarts
  - Labels: `system`, `dispatcher`, `actor_class`, `path`, `exception`

### Message Processing

- **`akka_actor_messages_received_total`**
  - Type: Counter
  - Description: Total number of messages received by actors
  - Labels: `system`, `actor_class`, `message_type`

- **`akka_actor_message_processing_time_seconds`**
  - Type: Histogram
  - Description: Time taken to process messages
  - Labels: `system`, `actor_class`, `message_type`
  - Buckets: 0.001, 0.005, 0.01, 0.025, 0.05, 0.1, 0.25, 0.5, 1, 2.5, 5, 10

### Mailbox Metrics

- **`akka_actor_mailbox_size`**
  - Type: Gauge
  - Description: Current number of messages in actor mailbox
  - Labels: `system`, `actor_class`, `path`

- **`akka_actor_stash_size`**
  - Type: Gauge
  - Description: Current number of messages in actor stash
  - Labels: `system`, `actor_class`, `path`

## Cluster Metrics

### Membership

- **`akka_cluster_members`**
  - Type: Gauge
  - Description: Current number of cluster members
  - Labels: `cluster`, `status` (up, joining, leaving, down, removed)

- **`akka_cluster_unreachable_members`**
  - Type: Gauge
  - Description: Number of unreachable cluster members
  - Labels: `cluster`

### Cluster Events

- **`akka_cluster_events_total`**
  - Type: Counter
  - Description: Total cluster events by type
  - Labels: `cluster`, `event_type`

### Sharding

- **`akka_cluster_sharding_regions`**
  - Type: Gauge
  - Description: Number of active shard regions
  - Labels: `cluster`, `type_name`

- **`akka_cluster_sharding_entities`**
  - Type: Gauge
  - Description: Number of active entities
  - Labels: `cluster`, `type_name`, `shard_id`

## Remote Metrics

### Connections

- **`akka_remote_connections`**
  - Type: Gauge
  - Description: Number of active remote connections
  - Labels: `system`, `direction` (inbound, outbound)

### Message Transfer

- **`akka_remote_messages_sent_total`**
  - Type: Counter
  - Description: Total messages sent to remote actors
  - Labels: `system`, `destination`

- **`akka_remote_messages_received_total`**
  - Type: Counter
  - Description: Total messages received from remote actors
  - Labels: `system`, `source`

- **`akka_remote_message_size_bytes`**
  - Type: Histogram
  - Description: Size of remote messages in bytes
  - Labels: `system`, `direction`

## Dispatcher Metrics

### Thread Pool

- **`akka_dispatcher_threads_active`**
  - Type: Gauge
  - Description: Number of active dispatcher threads
  - Labels: `system`, `dispatcher`

- **`akka_dispatcher_threads_total`**
  - Type: Gauge
  - Description: Total number of dispatcher threads
  - Labels: `system`, `dispatcher`

### Task Processing

- **`akka_dispatcher_queue_size`**
  - Type: Gauge
  - Description: Number of tasks in dispatcher queue
  - Labels: `system`, `dispatcher`

- **`akka_dispatcher_task_processing_time_seconds`**
  - Type: Histogram
  - Description: Time to process dispatcher tasks
  - Labels: `system`, `dispatcher`

## Persistence Metrics

### Journal

- **`akka_persistence_journal_events_persisted_total`**
  - Type: Counter
  - Description: Total events persisted to journal
  - Labels: `system`, `plugin`

- **`akka_persistence_journal_recovery_time_seconds`**
  - Type: Histogram
  - Description: Time taken for journal recovery
  - Labels: `system`, `plugin`, `persistence_id`

### Snapshot

- **`akka_persistence_snapshot_saves_total`**
  - Type: Counter
  - Description: Total snapshots saved
  - Labels: `system`, `plugin`

- **`akka_persistence_snapshot_loads_total`**
  - Type: Counter
  - Description: Total snapshots loaded
  - Labels: `system`, `plugin`

## System Metrics

### JVM/CLR

- **`process_cpu_seconds_total`**
  - Type: Counter
  - Description: Total CPU time consumed
  - Labels: `system`

- **`process_memory_bytes`**
  - Type: Gauge
  - Description: Process memory usage
  - Labels: `system`, `type` (heap, non-heap, gc)

- **`dotnet_gc_collections_total`**
  - Type: Counter
  - Description: Total garbage collections
  - Labels: `system`, `generation`

## Custom Application Metrics

Phobos also supports custom application metrics:

- **`application_custom_*`**
  - Various types supported
  - Description: Application-specific metrics
  - Labels: Defined by application

## Query Examples

### Message Processing Rate
```promql
rate(akka_actor_messages_received_total[5m])
```

### 95th Percentile Message Latency
```promql
histogram_quantile(0.95, 
  rate(akka_actor_message_processing_time_seconds_bucket[5m])
)
```

### Cluster Health
```promql
akka_cluster_members{status="up"} / 
ignoring(status) group_left 
sum(akka_cluster_members) by (cluster)
```

## Best Practices

1. **Use appropriate time ranges** for rate calculations (typically 5m or 10m)
2. **Apply filters** using labels to focus on specific components
3. **Use recording rules** for frequently-queried complex expressions
4. **Monitor cardinality** to prevent metric explosion
5. **Set up alerts** for critical thresholds

## Additional Resources

- [OpenTelemetry Metrics Specification](https://opentelemetry.io/docs/reference/specification/metrics/)
- [Prometheus Query Language](https://prometheus.io/docs/prometheus/latest/querying/basics/)
- [Phobos Monitoring Guide](https://phobos.petabridge.com/articles/monitoring/)
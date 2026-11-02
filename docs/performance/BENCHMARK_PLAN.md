# Performance Benchmark Plan

## Status
**No benchmark executed. All numbers below are targets or scenarios, not results.**

## Workload
1 Hz snapshot per host; initial 50 samples/batch; evaluate 10/30/50 batch sizes, 256/512/1024 B representative payloads and measured real samples. Each trial lasts at least 10 minutes, with warmup and repeat runs. Publish exact host OS, CPU, RAM, disk, TLS settings, HAProxy/Gateway/Kafka configuration, partition count and replication factor.

## Stages
- 1k snapshots/s (MVP)
- 10k snapshots/s (V1 aspiration)
- 50k snapshots/s (stretch)
- 100 to 1000+ sessions concurrently; use Little's Law to estimate socket demand.
- Fault tests: Gateway kill, PostgreSQL outage, Kafka outage, delayed ACK, reconnect storm, oversized frames, slow clients.

## Measurements
Agent send and ACK latency (p50/p95/p99), Gateway BatchEnd-to-ACK p99, throughput in snapshots/s, successful Kafka delivery, error/retry/unknown counts, max RSS, CPU %, fd count, queue depth, producer backlog, ClickHouse ingest lag, dropped/duplicate metrics. **Do not compare raw Protobuf throughput and JSON-transcoded throughput without labeling format.**

## Pass/fail
A target is passed only with actual trial output and documented no-data-loss caveats. Benchmarks must distinguish Kafka-confirmed ACK from ClickHouse persistence.

## Output
See `tests/results/RESULT_TEMPLATE.md` and `tests/results/README.md`.

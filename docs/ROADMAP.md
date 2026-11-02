# Delivery Roadmap

Each sprint must leave the project buildable/testable. Order is deliberate: test protocol and network core before adding distributed dependencies.

| Sprint | Artifact | Exit criteria |
|---|---|---|
| 01 | Contracts | Valid Protobuf envelope and golden vectors; build/test instructions |
| 02 | TCP core | LT epoll, framed reads, bounded resources; parser and integration tests |
| 03 | Publisher transport | Nonblocking batch client, 10s overall deadline, retryable errors |
| 04 | Kafka integration | Async producer, aggregate ACK, callback lifetime safety, partial delivery |
| 05 | Authentication | HAProxy TLS, PostgreSQL registry/cache, authorization, fail-closed behavior |
| 06 | Durable agent | SQLite WAL, 24h TTL, drop-oldest, crash recovery, jitter, 1Hz metrics |
| 07 | Analytics | ClickHouse, processor, query API, dedup strategy |
| 08 | HA/performance | Multi-node failures, reproducible profiling, benchmark report |

**Baseline performance targets (not measured):** MVP 1k snapshots/s; V1 10k snapshots/s; stretch 50k snapshots/s. Initial healthy-Kafka post-BatchEnd-to-ACK p99 aspiration under 300ms, only if benchmark configuration supports it.

# Later Sprint Work Packages

## Sprint 03: Publisher transport
Nonblocking TCP/TLS client, connect/handshake/auth/batch/ACK sequence, 10s overall deadline, retry same ID, deterministic timer/jitter tests.

## Sprint 04: Kafka
Async librdkafka integration, broker-confirmed delivery reports, per-record statuses, pending registry independent of socket lifetimes, queue pressure/unknown outcomes, out-of-order delivery tests.

## Sprint 05: Security
HAProxy TLS certificate/hostname validation; PostgreSQL Registry, async auth workers, bounded local cache, revocation reconciliation, rotation, cache-miss/failure tests, backend isolation.

## Sprint 06: Durable Agent
SQLite WAL, retention 24h max, drop-oldest, disk quota/headroom, boot recovery, rate-limited backlog drain, 1Hz Linux collectors. Measure actual serialized sizes before quota sizing.

## Sprint 07: Analytics
Kafka-to-ClickHouse contract, duplicate handling, raw retention + rollups, processor/query service, exactness of aggregates despite retries.

## Sprint 08: Fault tolerance + performance
3 Gateway nodes, HAProxy failover conditions, PostgreSQL interruption, Kafka crash, 10-minute repeatable load tests, recorded CPU/RSS/p99/errors, bottleneck profile and mitigation.

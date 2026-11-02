# Architecture Overview

## Domain
A Linux PC/server monitoring agent emits one `SystemMetricsSnapshot`/second (CPU, RAM, GPU, disk, network). Hybrid raw + derived metrics; total CPU raw counters and per-core usage. Sampling continues even during Kafka outage subject to local disk limits.

## Transport and reliability
- Agent stores unsent samples to SQLite WAL with max 24h TTL, drop-oldest under quota pressure. This is **bounded best-effort retention**, not guaranteed full 24-hour history.
- One short-lived TLS-protected TCP session per batch; length prefix 4-byte unsigned big endian + Protobuf transport frame.
- `AuthRequest` → `AuthResult` → `BatchStart` → telemetry frames → `BatchEnd` → `BatchAck`. One batch per connection.
- Agent overall session deadline 10 seconds (connect, TLS, auth, send, ACK).
- Ingest Gateway validates/authenticates before Kafka enqueue, streams records individually to async Kafka producer, aggregates Kafka delivery reports.
- Kafka-confirmed ACK does **not** mean ClickHouse persisted. Some records may be published even if batch failed or connection closed.
- Agent retries with same `(host_id, message_id)` when outcome unknown; downstream must handle duplicates.

## Gateway runtime
Single level-triggered `epoll` Reactor baseline. Reactor owns network fds and state. Kafka poll/auth workers communicate via bounded completion queue + eventfd; no worker may dereference a destroyed connection. All limits explicit: max frame, batch, connections, pending bytes and callbacks.

## Security
HAProxy terminates TLS 1.3, Agent validates server certificate + hostname. Gateway verifies per-agent API keys using PostgreSQL registry, bounded local cache, async lookups. Backend must be unreachable by untrusted clients; no trust in user-provided `host_id`. Registry outage: fresh cache may work; miss/expired fail closed. Revocation is eventually consistent and measured.

## Data platform
Kafka/Redpanda topic baseline `telemetry.system.metrics.v1` keyed by `host_id`; ClickHouse raw history, optional detail tables/rollups; analytics consumer independent. Decide Kafka Protobuf vs JSON, and precise dedup/downsample semantics before production use.

## Repository topology
`nexstream-contracts`, `nexstream-ingest`, `nexstream-publisher`, `nexstream-processor`, `nexstream-query`, `nexstream-deploy`.

## External boundaries
HAProxy is a critical component; 3 Gateway nodes do not provide HAProxy HA. Kafka/PG/ClickHouse availability must be evaluated independently. Not production-ready until TLS, authentication, durable queue, load tests, fault injection and alerting are verified.

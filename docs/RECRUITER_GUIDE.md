# Recruiter / Interviewer Guide

## Project pitch (30 seconds)
NexStream is a C++20 Linux telemetry pipeline: agents collect 1Hz host metrics, durably queue samples and transmit Protobuf batches via TLS-protected TCP to a nonblocking epoll Gateway that asynchronously publishes to Kafka/Redpanda. ClickHouse stores historical data. The project explores flow control, lifetime-safe callbacks, partial failures and repeatable performance tests.

## What to inspect
- Protocol/state machines: `docs/architecture/PROTOCOL.md`.
- Concurrency/lifetime strategy: `docs/architecture/OWNERSHIP_AND_FAILURES.md`.
- Security: `docs/security/SECURITY_MODEL.md`.
- Test inventory: `tests/TEST_CASES.md`.
- Actual run evidence: `tests/results/`.
- Engineering decisions: `docs/decisions/README.md`.

## Expected interview discussion
Explain `epoll` LT vs ET, partial TCP reads, `EAGAIN`, fd reuse, callback lifetime, Kafka ACK vs local queue acceptance, duplicate scenarios, memory backpressure, cache consistency, and what measured p99 means.

**Current status:** design documentation created; code and benchmarks are not yet implemented. Revise this section as evidence accumulates.

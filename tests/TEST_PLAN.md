# Test Plan and Quality Gates

## Levels
- Unit: endian/framing/decoder, state-machine, auth verification, retry policy, local queue retention.
- Integration: TCP publisher ↔ ingest, PostgreSQL auth, Kafka delivery report, SQLite crash recovery, ClickHouse ingestion.
- System/fault injection: Gateway restart, Kafka down, DB failover, auth revocation, slow clients, overload.
- Performance: throughput/p99/RSS/CPU with reproducible environment and duration.

## Required evidence for each execution
Date/time (UTC), git SHA(s), OS/toolchain, dependencies and versions, commands, configuration, dataset/workload, assertion outcomes, raw logs and artifacts, defects discovered.

## Exit criteria
No test marked PASS without execution. Expected results in catalog are specification, not observations. All critical security/decoder/reliability cases must pass for release; benchmarks separately reported with hardware context.

See `TEST_CASES.md` and `results/RESULT_TEMPLATE.md`.

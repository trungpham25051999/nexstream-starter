# Test Execution Report — TEMPLATE (NOT RUN)

- Run ID: `<YYYY-MM-DD>-<sprint>-<run>`
- Date/time UTC: `<timestamp>`
- Repository/revision(s): `<URL>` / `<git SHA>`
- Engineer / runner: `<name>`
- OS/kernel, CPU/RAM/disk: `<specs>`
- Compiler/CMake/Protobuf/dependency versions: `<versions>`
- Kafka brokers/partitions/replication/acks: `<configuration>`
- TLS/HAProxy/PG/CH configuration: `<configuration>`

## Scope and commands

```shell
# Paste exact commands executed here
```

## Results

| Test ID | Expected | Observed | PASS/FAIL/SKIP | Evidence |
|---|---|---|---|---|
| `<ID>` | `<criterion>` | `<actual observation>` | `<status>` | `<log path>` |

## Performance (only if executed)

- Test duration / warmup / repeats: `<value>`
- Payload schema and actual serialized bytes: `<value>`
- Snapshot throughput (received, Kafka-confirmed, ClickHouse committed): `<separate values>`
- Latency p50/p95/p99 (define start/end): `<values>`
- Max RSS, CPU usage, fd count: `<values>`
- Rejections/timeouts/retries/unknown/deduplicated: `<values>`
- Failure injection and recovery duration: `<values>`

## Conclusions and limitations

`<What evidence supports; what remains unproven; next actions>`

## Raw artifacts

`<Log names, dashboards, raw JSON/CSV output, flamegraphs, test trace paths>`

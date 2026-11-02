# Operational Runbook — Planned

## Startup (once implemented)
1. Check secrets/certificates in mounted files or secret manager, never inline in README.
2. Start PostgreSQL and Kafka/Redpanda; confirm health.
3. Start Gateway(s) with bounded limits; verify listener not exposed publicly.
4. Configure HAProxy; verify TLS chain, hostname and health checks.
5. Start Publisher; check queue age, ACK latency and error metrics.

## Fault handling
- Kafka down: no false success ACK; Gateway fast reject under pressure; Agent keeps local snapshots within TTL/quota and retries with jitter.
- PostgreSQL down: cache policy applies; fresh-cache auth allowed only until fixed freshness deadline, misses fail closed; monitor revocation lag.
- Gateway crash: Agent reconnects after backoff; Kafka duplicates possible for unknown ACKs.
- Disk full: drop-oldest and record dropped count; fail record persist explicitly when no capacity.
- TLS expiry: correct certificate/hostname; never disable verification.

Fill exact commands/ports once deployment exists. This is a design runbook, not a claim that infrastructure is deployed.

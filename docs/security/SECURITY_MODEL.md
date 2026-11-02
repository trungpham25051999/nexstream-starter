# Security and Trust Model

## Chosen baseline
TLS 1.3 at HAProxy + server certificate hostname verification at Agent; per-Agent API key verified at C++ Gateway. PostgreSQL Registry with bounded local cache and asynchronous lookup worker pool. Trust API key binding to authorized `host_id`, not `host_id` alone.

## Threats and countermeasures
- Impersonated server: certificate chain and hostname verification; no insecure-skip flag.
- Stolen credentials: unique high-entropy per-Agent keys, key rotation/revoke, no logs, secure file/OS store permissions.
- Credential replay: TLS, rate limits, revoked key policy; key compromise remains impersonation risk.
- Connection flood: edge DDoS/network controls, HAProxy limits, TLS handshake deadline, kernel capacity.
- App flood/slowloris: auth-first state machine, 1s auth budget candidate, bounded buffers and connection lifetime.
- Forged forwarded metadata: backend network isolation; use PROXY protocol only from trusted HAProxy.
- Revoked key in local cache: versioned cache, LISTEN/NOTIFY plus durable polling/reconciliation; define revocation-lag SLO.
- DB unavailable: fresh cache per explicit bounded freshness policy; misses/expired fail closed.
- HAProxy single instance is SPOF for MVP; multi-proxy HA is later work.

## Provisioning
Admin enrolls agent and host identity; secrets created via CSPRNG; store verifier (not raw secret) in PG; deliver secret once via trusted channel; agent protects local secret, restrict file permissions; allow dual-key rotation window; audit changes. Provisioning UI/service is not yet built.

## Important distinction
TLS termination plus API-key authentication does **not** prevent volumetric DDoS or guarantee downstream availability. Security tests are required in `tests/TEST_CASES.md`.

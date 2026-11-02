# TCP Protocol Specification — Draft for Implementation

## Framing
`uint32_be payload_length` (4 bytes) followed by serialized Protobuf `Frame` of exactly `payload_length` bytes. No delimiter, no implicit recv boundary. Reject payload length 0 and lengths above configured max (initial proposed 65536 bytes). Aggregate batch limit initially 1 MiB and max 50 samples, pending benchmark.

## One connection / one batch
`TCP connect → TLS handshake → AuthRequest → AuthResult → BatchStart → Telemetry* → BatchEnd → Kafka delivery resolution → BatchAck → close`.

Transport `Frame` oneof: `AuthRequest`, `AuthResult`, `BatchStart`, `SystemMetricsSnapshot` (or Telemetry envelope referencing it), `BatchEnd`, `BatchAck`, `ProtocolError`. Precise field numbers/error enum are Sprint 01 output, not yet frozen.

## Identity and ACK
- `AuthRequest` carries `key_id`, secret, asserted host identity; auth success binds session to authorized host.
- All snapshots in session must match authenticated host.
- Batch has stable `batch_id` (transport correlation), each sample stable `message_id` (dedup identity).
- `BatchAck`: report success/failed/unknown per index or ID, and possible `RETRY_LATER`; **SUCCESS is conditional on Kafka broker delivery confirmation**.
- If socket disappears after Kafka delivery, Agent will retry; downstream must dedup.
- Batch is not atomic; session timeout cannot retract in-flight Kafka records.

## Decoder behavior
- Partial 1–3 byte headers, fragmented payloads and several frames per `recv` must work.
- Validate length before allocation. Apply memory budgets, deadline, frame count and parser checks.
- Check state transition before accepting frame type. On malformed frame fail closed, produce no unauthorized telemetry.
- Avoid CPU starvation from one extremely active connection: per-tick frame/byte budget and Reactor fairness.

## Security boundaries
TLS is terminated by HAProxy; backend must be private or mutually authenticated to proxy. No client-supplied trusted forwarded identity. No API keys in logs. Never expose plaintext backend listener publicly.

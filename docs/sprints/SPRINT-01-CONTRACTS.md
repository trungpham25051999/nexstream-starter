# Sprint 01 — Protobuf Contracts

## Goal
Create `nexstream-contracts` with versioned transport envelopes and a minimal `SystemMetricsSnapshot` schema. Avoid implementing full Linux collectors in this sprint.

## Tasks
1. Define `nexstream.transport.v1.Frame` oneof for AuthRequest, AuthResult, BatchStart, Telemetry, BatchEnd, BatchAck, ProtocolError.
2. Define stable IDs: agent ID/host ID/batch ID/message ID and result codes incl. SUCCESS, RETRYABLE_FAILURE, PERMANENT_FAILURE, UNKNOWN, RETRY_LATER. Distinguish AuthResult from BatchAck.
3. Define minimal `nexstream.telemetry.v1.SystemMetricsSnapshot` (identity, sample timestamp, one CPU/memory field) and extension-safe field numbering. Detailed CPU/GPU schema is later additive.
4. Set explicit bounds in protocol docs (message lengths, batch count, identifier sizes, max auth-frame bytes). Avoid writing secrets to logs.
5. Add CMake/protoc build, generated headers as build artifacts, schema lint/compatibility checks if available.
6. Golden vectors for valid frames + malformed/unknown enum/forward-compatible parsing.
7. Update README with exact build commands **only after verifying them**.

## Test cases
TC-PROTO-001..006 in `tests/TEST_CASES.md`.

## Definition of done
Build succeeds; sample serialized/deserialized with equal semantic data; frame oneof validated; versioned proto packages; golden vector tests pass and results recorded.

## Scope guard
Implement Sprint 01 only: plan, code, tests, build logs and a concise review. Do not implement Gateway, Kafka or security integrations prematurely.
